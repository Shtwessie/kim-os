# Activer Kim, l'agent d'accueil du portfolio

Kim fonctionne déjà en **mode démo** (réponses préparées). Pour qu'il réponde vraiment avec Claude et envoie les audits par e-mail, il suffit d'activer ce workflow sur ton instance n8n (`semarjedjiga.app.n8n.cloud`).

## 1. Importer
n8n → **Workflows → Import from file** → `kimos-agent-workflow.json`.

## 2. Brancher les 3 identifiants
| Nœud | Identifiant à choisir |
|---|---|
| Claude · conversation / diagnostic / e-mail d'audit | **Header Auth** — Name : `x-api-key`, Value : ta clé API Anthropic (console.anthropic.com). Même identifiant pour les 3 nœuds. |
| E-mail au visiteur, Alerte à Shtwessie | Ton compte **Gmail** (OAuth). |
| Journal des leads (Sheets) | Ton compte **Google Sheets**, puis colle l'URL d'une feuille avec les colonnes : `Date, Nom, E-mail, Entreprise, Tâche, Volume / mois, Minutes, Gain h/an, Gain €/an, Statut`. |

## 3. Activer
Bascule **Active** en haut à droite. L'adresse de production doit être :
`https://semarjedjiga.app.n8n.cloud/webhook/kimos-agent` (c'est celle que le portfolio appelle).

Dès que c'est actif, le badge de Kim passe à **« En ligne · n8n × Claude »**.

## Protections intégrées
- 25 messages max par visiteur et par heure, 400 par jour, 30 e-mails d'audit par jour.
- Seul le site `https://shtwessie.github.io` peut appeler le webhook (CORS).
- La clé Anthropic reste dans n8n, jamais dans la page publique.
- Kim refuse de sortir de son rôle et n'invente ni tarif ni client.
- Chaque message consomme une exécution n8n et quelques centimes de crédits Claude (modèle Haiku).

## Tester
Ouvre le portfolio, fais un diagnostic avec ton propre e-mail : tu dois recevoir l'audit, l'alerte, et voir une ligne dans la feuille.
