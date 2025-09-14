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
