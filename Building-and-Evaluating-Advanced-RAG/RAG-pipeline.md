## Contexte général : qu’est‑ce qu’un "Query Engine" en RAG ?

Le **RAG (Retrieval‑Augmented Generation)** est un système qui, à partir d'une question de l’utilisateur, récupère des extraits de documents pertinents, puis les envoie à un LLM (comme GPT-3.5) pour générer une réponse.

Un **query engine**, dans ce contexte, est un composant qui effectue deux étapes principales :

1. **Récupération** (retrieval) : retrouve des passages pertinents dans une base de documents.
2. **Synthèse** (synthesis) : envoie ces extraits + la question au LLM pour obtenir la réponse.

Dans le cours, trois variantes de ce moteur sont présentées : **Direct Query Engine**, **Sentence Window Query Engine**, et **Auto‑Merging Query Engine**. Voyons comment ils diffèrent.

---

## 1. **Direct Query Engine** (RAG de base)

C’est la version la plus simple. Le pipeline fonctionne ainsi :

1. Le document est **haché en chunks** (morceaux de taille fixe).
2. On indexe ces chunks dans une base de vecteurs.
3. À une requête, on récupère les *K* chunks les plus proches (top‑K).
4. On envoie directement ces morceaux + la question à l’LLM.

\*\* Avantage\*\* : facile à implémenter.
\*\* Limite\*\* : les chunks peuvent manquer de contexte, ou être trop courts, et parfois la cohérence globale est faible.
([DeepLearning.AI - Learning Platform][1])

---

## 2. **Sentence Window Query Engine**

Ici, on améliore la gestion du contexte en deux étapes :

1. **Retrieval** sur des morceaux très petits : des phrases individuelles ou chunks minimalistes.
2. Lors de la synthèse (synthesis), on **remplace** la phrase récupérée par un **fenêtre contextuelle** : la phrase plus les phrases autour (avant et après).

Cela donne un contexte plus riche au LLM sans perdre en précision à l’étape de recherche.
([DeepLearning.AI - Learning Platform][2])

\*\* Avantages\*\* :

* Plus de contexte pour le LLM, donc généralement des réponses plus pertinentes (meilleure *groundedness* et *context relevance*) ;
* Garde la précision du retrieval grâce à l’embedding de petites phrases.

\*\* Attention\*\* : plus on agrandit la fenêtre (par exemple 1 phrase → 3 → 5), plus le coût (tokens, latence) augmente. Au-delà d’une certaine taille, la qualité peut baisser car le LLM peut s’embrouiller.
([DeepLearning.AI - Learning Platform][2])

---

## 3. **Auto‑Merging Query Engine**

Cette approche utilise une **hiérarchie de chunks** :

* On définit des **chunks enfants** (petits) et des **chunks parents** (plus larges, composés des enfants).
* Pendant la requête, si plusieurs enfants d’un même parent sont récupérés, on les **fusionne** automatiquement en un chunk parent : plus cohérent et moins fragmenté.

Exemple : quatre petits chunks enfants peuvent être remplacés par un chunk parent plus long et fidèle à l’ensemble.
([DeepLearning.AI - Learning Platform][3])

\*\* Avantages\*\* :

* Less fragmentation of information.
* Aids coherence and reduces redundant context.
* Maintains efficiency by substituting multiple pieces with one coherent piece.

---

## Résumé comparatif

| Query Engine            | Étape de retrieval                    | Contextualisation pour LLM           | Points forts                                |
| ----------------------- | ------------------------------------- | ------------------------------------ | ------------------------------------------- |
| **Direct Query Engine** | Chunks classiques                     | Aucun ajout de contexte              | Simple, rapide                              |
| **Sentence Window**     | Phrases (ou petits chunks)            | Fenêtre autour de la phrase          | Contexte plus riche, meilleur soutien       |
| **Auto‑Merging**        | Chunks hiérarchiques (petits+parents) | Regroupement automatique des enfants | Moins de fragmentation, cohérence renforcée |

---

## En résumé, en mots simples :

* **Direct Query Engine** : tu récupères des bouts de texte, tu les envoies à l’LLM. Rapide mais parfois trop décousu.
* **Sentence Window** : tu repères une phrase clé, et tu la complètes avec ce qui la précède et suit, pour plus de sens.
* **Auto‑Merging** : si plusieurs morceaux importants appartiennent à un même gros bloc, tu les remplaces par ce gros bloc, plus cohérent.
