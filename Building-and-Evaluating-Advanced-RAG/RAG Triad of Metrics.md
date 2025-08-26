# Explication des trois métriques (RAG Triad)

| Métrique              | Définition simple                                                             | Pourquoi c’est intéressant                                                                |
| --------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Context Relevance** | Est-ce que les passages récupérés sont pertinents par rapport à la question ? | Éviter que le modèle hallucine à cause de contexte inadapté               |
| **Groundedness**      | L’énoncé donné par le modèle est-il bien soutenu par le contexte récupéré ?   | Vérifier la cohérence factuelle avec les sources        |
| **Answer Relevance**  | La réponse est-elle bien centrée sur ce que l’utilisateur a demandé ?         | Contrôler l’adéquation au besoin réel de l’utilisateur  |

En gros : **Context Relevance** vérifie la qualité du *retrieval*, **Groundedness** l’adéquation entre ce qui est dit et ce qui est fourni, et **Answer Relevance** assure que la réponse est vraiment utile au bon endroit.

---

### Pour aller plus loin

* La **page de DeepLearning.AI** confirme l’importance de cette triade dans l’évaluation et l’itération durable du pipeline RAG ([DeepLearning.AI][4]).
* **TruLens** est mis en œuvre pour configurer, logguer, et analyser facilement ces métriques au sein d’une expérience interactive ([DeepLearning.AI - Learning Platform][1]).

---

### En résumé

La vidéo *"RAG Triad of Metrics"* explique comment :

* Construire un pipeline RAG avec **Llama Index** et le lancer avec une question.
* Utiliser **TruLens** pour mesurer \*\* trois dimensions cruciales\*\* (Context Relevance, Groundedness, Answer Relevance).
* Visualiser ces métriques via un tableau de bord interactif pour comprendre les forces et les faiblesses du système RAG.
