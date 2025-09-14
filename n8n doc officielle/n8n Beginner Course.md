# n8n Beginner Course (1/9) - Introduction to Automation

## Qu'est-ce que l'automatisation ?
L’automatisation consiste à **remplacer des tâches manuelles répétitives par des processus automatiques**.  
Au lieu de cliquer, copier-coller ou vérifier des données soi-même, un système (comme n8n) exécute les actions à notre place.

## Pourquoi automatiser ?
- **Gagner du temps** (ne pas répéter les mêmes tâches)
- **Réduire les erreurs humaines**
- **Se concentrer sur des tâches à plus forte valeur ajoutée**

## Exemples d’automatisation avec n8n
1. **Réseaux sociaux**  
   - Quand un nouvel article est publié sur un blog → le partager automatiquement sur Twitter, LinkedIn, etc.
2. **E-commerce**  
   - Lorsqu’un client passe une commande → envoyer les infos vers Google Sheets + notifier sur Slack.
3. **Email & CRM**  
   - Quand un email arrive avec une pièce jointe → sauvegarder automatiquement la pièce dans Google Drive.

## Pourquoi n8n ?
- Pas besoin de savoir coder pour créer des **workflows visuels**.
- Plus flexible que Zapier/Make car tu peux aller beaucoup plus loin avec des conditions, du code personnalisé, et des intégrations plus variées.
- Open-source → tu peux l’héberger toi-même ou utiliser leur cloud.

---

✅ **Idée clé du cours** :  
L’automatisation avec n8n, c’est créer des workflows qui prennent en entrée un **événement déclencheur** (ex. un nouvel email) et enchaînent des **actions automatiques** (ex. sauvegarder l’email + notifier sur Slack).



# n8n Beginner Course (2/9) - Introduction to APIs and Webhooks

## Qu'est-ce qu'une API ?
- Une **API (Application Programming Interface)** est une manière pour deux applications de communiquer entre elles.  
- Elle permet d’automatiser des échanges de données sans intervention humaine.

### Exemple simple :
- Une API météo → tu lui envoies le nom d’une ville, elle te renvoie la température.  
- Une API de Google Sheets → tu peux ajouter une ligne dans un tableau automatiquement.

---

## Qu'est-ce qu’un Webhook ?
- Un **webhook** est comme une **alerte envoyée par une application** quand quelque chose se produit.  
- Plutôt que d’aller vérifier toutes les minutes, l’app t’envoie directement l’info.

### Exemple simple :
- Stripe envoie un webhook quand un paiement est réussi.  
- Shopify envoie un webhook quand un client passe une commande.  
- Tu peux connecter ce webhook dans n8n pour déclencher un workflow (ex. ajouter le client dans ton CRM + envoyer un email).

---

## API vs Webhook (comparaison)
- **API** → tu demandes l’info (ex. “Quelle est la météo à Paris ?”).  
- **Webhook** → l’info vient à toi automatiquement quand elle change (ex. “Un nouvel utilisateur s’est inscrit”).  

---

## Exemples d’utilisation avec n8n
1. **Webhook d’inscription utilisateur**  
   - Un webhook reçoit les infos d’un nouvel inscrit → n8n les ajoute dans Google Sheets + envoie un mail de bienvenue via Gmail.
2. **API d’un réseau social**  
   - n8n interroge l’API de Twitter → récupère les derniers tweets avec un mot-clé → les envoie sur Slack.

---

✅ **Idée clé du cours** :  
- Les **APIs** permettent à n8n d’aller chercher des données.  
- Les **webhooks** permettent à n8n d’être notifié automatiquement d’un événement.  
En combinant les deux, on peut créer des workflows puissants et réactifs.



# n8n Beginner Course (3/9) - What are Nodes?

## Qu’est-ce qu’un "node" ?
- Un **node** est un **bloc de construction** dans n8n.  
- Chaque node représente **une action spécifique** dans un workflow.  
- Un workflow est donc une **suite de nodes reliés entre eux**.

---

## Types de nodes
1. **Trigger Nodes (déclencheurs)**  
   - Démarrent un workflow quand un événement se produit.  
   - Exemple : un **Webhook node** qui se déclenche quand un formulaire est rempli.

2. **Action Nodes**  
   - Effectuent une tâche spécifique.  
   - Exemple : un **Gmail node** pour envoyer un email, ou un **Google Sheets node** pour ajouter une ligne.

3. **Logic Nodes**  
   - Permettent d’ajouter de l’intelligence au workflow.  
   - Exemple : **IF node** (si/alors) → si le client dépense plus de 100 €, alors envoyer un message spécial.

---

## Exemple concret
- **Webhook node** → reçoit un nouvel achat en ligne.  
- **IF node** → vérifie si le montant est supérieur à 100 €.  
- **Google Sheets node** → ajoute les infos du client dans un tableau.  
- **Email node** → envoie un message de remerciement personnalisé.  

---

## Pourquoi les nodes sont importants ?
- Ils permettent de **visualiser clairement** ce que fait ton automatisation.  
- Ils rendent le workflow **modulaire** : tu peux facilement ajouter, retirer ou modifier une étape.  
- Pas besoin de coder → tout se fait via des blocs visuels.

---

✅ **Idée clé du cours** :  
Un workflow n8n est comme une **chaîne de blocs (nodes)** où chaque node a un rôle précis (déclencher, agir, décider).  
Les nodes sont l’élément central de n8n : tout passe par eux.


# n8n Beginner Course (4/9) - How does n8n handle data?

## Comment n8n gère les données
- Chaque **node** reçoit des **données en entrée** et produit des **données en sortie**.  
- Les données circulent **d’un node au suivant** tout au long du workflow.

## Structure des données
- Les données sont organisées en **items** (semblables à des objets **JSON**).  
- Un item = des **paires clé–valeur**.

Exemple d’item :  
- name: Alice  
- email: alice@example.com  
- amount: 120  

## Flux des données (vue d’ensemble)
1. **Trigger node** → fournit les premières données (webhook, cron, événement…).  
2. **Action/Transformation** → enrichit ou modifie les champs (ex. ajouter `status`).  
3. **Sortie** → envoie vers un service externe (Sheets, Email, DB, API…).  

## Exemple concret
1. **Webhook** reçoit :  
   - name: Alice  
   - email: alice@example.com  
   - amount: 120  

2. **IF** vérifie : `amount > 100`.  
3. **Google Sheets** ajoute une ligne avec `name`, `email`, `amount`.  
4. **Email** envoie un message personnalisé si la condition est vraie.  

## Points importants
- Chaque node peut **lire** et **modifier** les champs qu’il reçoit.  
- Les sorties d’un node sont **réutilisables** par les nodes suivants.  
- Tu peux **inspecter** la sortie de chaque node dans l’UI pour déboguer.  

## Expressions utiles (référencer les données)
- Lire un champ JSON : `{{$json["email"]}}` ou `{{$json.email}}`  
- Combiner du texte + données :  
  - Titre : `Bienvenue {{$json.name}} !`  
  - Montant formaté : `{{$json.amount}} €`  
- Accéder à la sortie d’un node spécifique :  
  - `{{ $node["Webhook"].json.name }}`  

---

✅ **Idée clé du cours**  
n8n manipule des **items JSON** qui transitent de node en node.  
Tu utilises des **expressions** pour piocher les bons champs au bon moment, transformer les données, puis les envoyer là où il faut.

# n8n Beginner Course (5/9) - Core Workflow Concepts

## Objectif du cours
Découvrir les **concepts fondamentaux** qui permettent de comprendre et construire des workflows efficaces dans n8n.

---

## Les éléments clés d’un workflow

### 1. Trigger (déclencheur)
- Premier node du workflow.  
- Il démarre le processus quand un événement se produit.  
- Exemples :  
  - Un webhook reçoit des données d’un formulaire.  
  - Un cron job se déclenche tous les matins à 9h.

### 2. Actions
- Les nodes qui exécutent des tâches spécifiques.  
- Exemples :  
  - Envoyer un email.  
  - Ajouter une ligne dans Google Sheets.  
  - Poster un message sur Slack.

### 3. Données qui circulent
- Chaque node **reçoit des données en entrée** et renvoie des **données en sortie**.  
- Ces données peuvent être réutilisées dans les nodes suivants.

### 4. Expressions
- Utilisées pour insérer des données dynamiques dans les nodes.  
- Exemple :  
  - `Bienvenue {{$json.name}} !` → personnalise un email avec le prénom de l’utilisateur.

### 5. Branches logiques
- Les workflows peuvent prendre des chemins différents selon les conditions.  
- Exemple :  
  - **IF node** → si montant > 100 €, envoyer un email VIP.  
  - Sinon → envoyer un email standard.

---

## Exemple concret
1. **Webhook trigger** → reçoit une nouvelle commande (nom, email, montant).  
2. **IF node** → vérifie si le montant est supérieur à 100 €.  
3. **Google Sheets node** → enregistre la commande.  
4. **Email node** → envoie un message personnalisé selon la condition.  

---

✅ **Idée clé du cours**  
Un workflow est composé d’un **trigger** qui démarre le processus, suivi d’une série de **nodes** (actions, conditions, transformations) qui manipulent et transmettent les données jusqu’à produire le résultat attendu.


# n8n Beginner Course (6/9) - Useful Nodes in n8n

## Objectif du cours
Découvrir quelques **nodes fréquemment utilisés** dans n8n pour construire rapidement des workflows utiles.

---

## Catégories de nodes utiles

### 1. Trigger Nodes
- **Webhook** : démarre un workflow quand une application externe envoie des données.  
- **Cron** : déclenche un workflow à une heure ou fréquence précise (ex. tous les jours à 8h).  

### 2. Communication
- **Email (Send Email / Gmail)** : envoyer automatiquement des emails personnalisés.  
- **Slack / Microsoft Teams** : poster des messages sur des canaux internes.  

### 3. Données & stockage
- **Google Sheets** : ajouter, lire ou mettre à jour des lignes dans un tableau.  
- **Airtable** : gérer des bases de données simples pour organiser des infos.  
- **Database nodes** (MySQL, Postgres, etc.) : interagir directement avec des bases de données.  

### 4. Logic & transformation
- **IF** : exécuter des actions conditionnelles (si/alors).  
- **Switch** : router les données selon plusieurs cas possibles.  
- **Set** : créer ou modifier des champs spécifiques dans les données.  
- **Function** : écrire un peu de code personnalisé en JavaScript si besoin.  

### 5. APIs & intégrations
- **HTTP Request** : interagir avec n’importe quelle API REST (très puissant pour connecter des apps non supportées nativement).  

---

## Exemple concret de workflow avec nodes utiles
1. **Cron trigger** → démarre chaque matin à 9h.  
2. **HTTP Request** → récupère les dernières données d’une API météo.  
3. **IF node** → vérifie si la météo prévoit de la pluie.  
4. **Slack node** → envoie un message automatique à l’équipe :  
   - "Prenez vos parapluies aujourd’hui !"  

---

✅ **Idée clé du cours**  
Quelques nodes suffisent pour couvrir la majorité des cas d’usage : **Webhook, Cron, Google Sheets, Email, HTTP Request, IF**.  
Les maîtriser, c’est avoir déjà une boîte à outils très puissante pour automatiser ses tâches.


# n8n Beginner Course (7/9) - Error Handling

## Objectif du cours
Apprendre à gérer les erreurs dans n8n afin que les workflows soient **fiables** et ne s’arrêtent pas brutalement en cas de problème.

---

## Pourquoi gérer les erreurs ?
- Les erreurs sont inévitables (API indisponible, mauvais format de données, email invalide…).  
- Sans gestion d’erreur, le workflow peut échouer et bloquer.  
- Avec des stratégies d’erreur, on garde le contrôle et on peut agir automatiquement.

---

## Options de gestion d’erreur

### 1. Error Workflow
- n8n permet de créer un **workflow spécial** qui se déclenche dès qu’une erreur survient dans un autre workflow.  
- Utile pour :  
  - Recevoir une notification par email ou Slack.  
  - Sauvegarder l’erreur dans Google Sheets pour suivi.  

### 2. Always Output Data
- Option qui permet à un node de **toujours renvoyer une sortie**, même si une erreur survient.  
- Exemple : si un email échoue, le workflow continue avec une info du type *“erreur : email non envoyé”*.  

### 3. Try/Catch avec des nodes logiques
- Utiliser des nodes comme **IF** ou **Switch** pour vérifier des conditions avant de lancer une action risquée.  
- Exemple : vérifier que l’adresse email existe avant d’essayer d’envoyer un mail.  

### 4. Retry on Fail
- Certains nodes proposent des **retries automatiques** si l’action échoue (ex. réessayer après quelques secondes).  

---

## Exemple concret
1. Workflow principal : envoi d’emails via Gmail.  
2. Si un envoi échoue → déclenchement d’un **Error Workflow**.  
3. Error Workflow :  
   - Notifie l’admin via Slack.  
   - Log l’erreur dans Google Sheets.  

---

✅ **Idée clé du cours**  
La gestion des erreurs rend les workflows **résilients**.  
Au lieu de s’arrêter sur une erreur, n8n peut la capturer, la documenter et continuer à fonctionner.


# n8n Beginner Course (8/9) - Debugging

## Objectif du cours
Comprendre comment **déboguer un workflow** dans n8n, c’est-à-dire trouver et corriger les erreurs ou comportements inattendus.

---

## Outils de débogage dans n8n

### 1. Exécuter un workflow étape par étape
- Tu peux lancer ton workflow en mode **exécution manuelle**.  
- Cela permet de voir la sortie de chaque node **individuellement**.

### 2. Inspecter les données
- Dans chaque node, onglet **Output**, tu peux visualiser les données reçues et envoyées.  
- Exemple : vérifier qu’un champ `email` contient bien une adresse avant de l’envoyer au node "Send Email".

### 3. Afficher les erreurs
- Si un node échoue, n8n montre un message d’erreur détaillé (ex. “401 Unauthorized” pour une API).  
- Ces infos aident à comprendre la cause : mauvais identifiant, clé API manquante, mauvais format…

### 4. Logger les données
- Utiliser des nodes comme **NoOp** (no operation) ou **Set** pour afficher/intercepter les données sans les modifier.  
- Utile pour vérifier la logique d’un workflow complexe.

### 5. Réexécuter avec les mêmes données
- n8n permet de **relancer un workflow** avec exactement les mêmes données d’entrée.  
- Pratique pour tester des corrections sans avoir à générer de nouveaux événements.

---

## Exemple concret de débogage
1. Tu crées un workflow : Webhook → Google Sheets → Email.  
2. L’email échoue car `{{$json.email}}` est vide.  
3. Tu ouvres le **Webhook node** et constates que la donnée reçue s’appelle `userEmail` au lieu de `email`.  
4. Tu corriges l’expression dans le node Email : `{{$json.userEmail}}`.  
5. Tu relances avec les mêmes données → le problème est résolu.  

---

✅ **Idée clé du cours**  
Le débogage consiste à **tester étape par étape**, inspecter les **données qui circulent**, et utiliser les outils de n8n pour comprendre où ça coince et corriger rapidement.



# n8n Beginner Course (9/9) - Collaboration

## Objectif du cours
Apprendre comment travailler en **équipe** avec n8n et partager ses workflows de manière efficace.

---

## Pourquoi la collaboration est importante ?
- Les automatisations concernent souvent **plusieurs équipes** (marketing, support, IT…).  
- Pouvoir **partager, documenter et gérer les workflows ensemble** permet d’éviter les doublons et les erreurs.  

---

## Outils et fonctionnalités de collaboration dans n8n

### 1. Partage de workflows
- Tu peux **exporter** un workflow en fichier JSON.  
- Ce fichier peut être importé par un collègue pour réutiliser ou modifier le workflow.  
- Pratique pour partager des modèles ou déployer d’un environnement à un autre (test → production).  

### 2. Versions et historique
- n8n garde un **historique des exécutions**.  
- Cela permet de voir qui a modifié quoi et quand, et de revenir en arrière si nécessaire.  

### 3. Documentation intégrée
- Il est conseillé d’ajouter des **notes et descriptions** dans les workflows.  
- Exemple : ajouter un **Sticky Note node** pour expliquer la logique.  

### 4. Collaboration en équipe (n8n Cloud / Self-hosted avancé)
- n8n Cloud permet de créer des **espaces d’équipe**.  
- Plusieurs utilisateurs peuvent collaborer sur les mêmes workflows.  
- Gestion des rôles : admin, éditeur, lecteur.  

---

## Exemple concret
- Une équipe marketing crée un workflow qui poste automatiquement sur les réseaux sociaux.  
- Elle exporte le workflow en JSON et le partage avec l’équipe support.  
- Le support l’adapte pour envoyer aussi une notification interne sur Slack.  
- Les deux équipes collaborent sur la même base sans repartir de zéro.  

---

✅ **Idée clé du cours**  
La collaboration dans n8n repose sur le **partage des workflows**, la **documentation claire** et l’utilisation d’outils comme l’export/import ou les espaces d’équipe.  
Cela permet de travailler efficacement à plusieurs sur les mêmes automatisations.
