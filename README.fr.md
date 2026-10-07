🇪🇸 [Versión en español](README.md) · 🇬🇧 [English version](README.en.md)

# Bayesian Compose v1.3.0

Composition épistémique de messages pour Claude Cowork et Claude Code.

> **Compatible avec [Agent Plugins 1.0.0](https://agent-plugins.org/specification)** — le format portable de distribution de l’Agentic AI Foundation (OpenAI, Amazon,
> Microsoft, Cursor et Vercel, avec Google comme *core maintainer*).
> Le paquet contient le manifeste portable `plugin.json` à la racine du plugin et
> le skill dans `plugins/bayesian-compose/skills/bayesian-compose/SKILL.md`, ce qui permet à tout client conforme de le découvrir.
>
> **Fonctionne dans ChatGPT.** Le skill est du texte : des instructions et des critères, sans
> exécution locale. Pour l’installer, active **Work** dans le sélecteur de ChatGPT et
> ajoute-le depuis **Compléments**, par son nom ou par l’URL de ce dépôt.
> Il fonctionne de la même manière que dans Claude. Son frontmatter
> respecte l’ensemble fermé de champs d’[Agent Skills](https://agentskills.io/specification),
> que ChatGPT, claude.ai et la Skills API exigent pour accepter l’importation
> — une clé supplémentaire n’est pas ignorée, elle provoque une erreur bloquante. Les skills sont aussi disponibles dans l’
> **offre gratuite**, avec des limites d’utilisation.

## Ce qu’il fait

Il t’interroge avant de rédiger un message (email, Slack, WhatsApp, lettre,
tout type de texte) pour maximiser sa qualité épistémique. Il évalue le brouillon obtenu
selon 30 critères de rationalité bayésienne (LessWrong Sequences), du point de vue de la
**perspective estimée du destinataire** — pas de la tienne.

Ce n’est pas un outil de reformulation d’emails. C’est un exercice d’**empathie épistémique** : il t’oblige
à réfléchir depuis l’autre côté avant d’écrire.

## Philosophie

La plupart des outils de rédaction demandent « est-ce bien formulé ? ». Ce plugin
pose une autre question :

- Est-ce que cela change quelque chose de concret pour le destinataire ? (Value of Information)
- Est-ce que je lui dis quelque chose auquel il ne s’attendait pas ? (Bayesian Surprise)
- Est-ce que j’inclus toutes les preuves, ou seulement celles qui m’arrangent ? (Filtered Evidence)
- Est-ce que j’explore vraiment ou est-ce que je cherche une validation ? (Forward vs Backward Flow)
- L’urgence est-elle réelle ou fabriquée ? (Real vs Manufactured Urgency)
- Le message s’appuie-t-il sur des faits vérifiables ? (Entangled Truths)
- Ai-je décidé d’abord et raisonné ensuite ? (Fake Justification)
- Y a-t-il quelque chose de gênant que je passe sous silence ? (Absence of Expected Evidence)

Le résultat n’est pas un joli texte, mais un message qui **mérite l’attention
du destinataire** — évalué avec les mêmes 30 critères que le plugin
[email-triage](https://github.com/novanoticia/email-triage-plugin) utilise pour
filtrer les emails entrants.

## Relation avec Email Triage

Ce sont les deux faces d’une même démarche épistémique :

| | Email Triage | Bayesian Compose |
|---|---|---|
| **Direction** | Messages que tu reçois | Messages que tu envoies |
| **Question** | « Mérite-t-il mon attention ? » | « Mérite-t-il l’attention du destinataire ? » |
| **Critères** | 30 (rationalité bayésienne) | Les mêmes 30, inversés pour l’envoi |
| **Perspective** | La tienne (destinataire) | Celle de l’autre (destinataire estimé) |

Ce sont des outils indépendants. Aucun ne nécessite l’installation de l’autre. Mais
si les deux sont actifs, ils forment un système bidirectionnel : tu filtres ce que tu reçois
avec rigueur épistémique et tu envoies avec la même rigueur.

## Fonctionnement

### 1. Entretien socratique (5+1 questions)

Avant d’écrire quoi que ce soit, le skill te pose des questions qui correspondent aux critères
épistémiques les plus importants :

| # | Question | Ce qu’elle évalue |
|---|----------|------------|
| 1 | **Que veux-tu que le destinataire FASSE ?** | S’il y a une action concrète (GATE : sinon, le message ne devrait peut-être pas exister) |
| 2 | **Quelle est la décision réelle concernée ?** | Si tu parles de la décision ou si tu tournes autour |
| 3 | **Quels faits vérifiables étayent cela ?** | S’il y a des points d’appui vérifiables (dates, indicateurs, tickets) |
| 4 | **Y a-t-il quelque chose que tu devrais inclure mais que tu préférerais omettre ?** | Si tu filtres les preuves (la question la plus importante) |
| 5 | **Que se passe-t-il si le destinataire le lit demain plutôt que maintenant ?** | Si l’urgence est réelle ou fabriquée |
| 6 | **Qui reçoit ce message et que sait déjà cette personne ?** | Distance inférentielle et adaptation au destinataire (facultatif) |

La **question 1 est un gate** : s’il n’y a pas d’action concrète, le skill te propose de
repenser le message, de continuer avec un Score attendu faible ou de ne pas encore l’envoyer.

### 2. Brouillon guidé

À partir de tes réponses, Claude génère un brouillon qui :
- Commence par l’action/la décision (pas par le contexte)
- S’appuie sur des faits vérifiables
- Inclut les informations gênantes, s’il y en a
- Adapte la complexité au destinataire
- N’utilise pas de jargon qui bloque la réflexion

Le brouillon est un **guide, pas un texte définitif**. Il le réécrit sur demande.

### 3. Diagnostic selon 30 critères

Il évalue le brouillon selon les 30 critères, toujours tous, regroupés en 4 axes :

**Groupe A — Valeur de l’information**
| # | Critère | Poids |
|---|----------|------|
| 1 | Change quelque chose de concret | ±5 |

**Groupe B — Mise à jour bayésienne**
| # | Critère | Poids |
|---|----------|------|
| 2 | Changement des prédictions | ±4 |
| 3 | Surprise bayésienne | ±3 |
| 4 | Preuves filtrées | -3 |
| 5 | Forward/Backward flow | ±3 |

**Groupe C — Conception attentionnelle et utilité**
| # | Critère | Poids |
|---|----------|------|
| 6 | Retour sur l’attention | ±2 |
| 7 | Confusion productive | +4 |
| 8 | Impact causal réel | +4 |
| 9 | Bruit social | -3 |
| 10 | Ouvre des possibilités | +3 |
| 11 | Distance inférentielle | -2 |
| 12 | Agent stratégique | -3 |
| 13 | Densité informationnelle | ±2 |
| 14 | Urgence réelle ou fabriquée | ±3 |
| 15 | Pertinence à long terme | +4 |

**Groupe D — Lutte contre les biais et qualité de l’argumentation**
| # | Critère | Poids |
|---|----------|------|
| 16 | Motivated stopping | -2 |
| 17 | Motivated continuation | -2 |
| 18 | True rejection | ±2 |
| 19 | Third alternative | +3 |
| 20 | Privileging the hypothesis | -3 |
| 21 | Proper humility | ±3 |
| 22 | Positive bias | -2 |
| 23 | Argument screens off authority | ±3 |
| 24 | Hug the query | ±4 |
| 25 | Semantic stopsigns | -3 |
| 26 | Fake justification | -3 |
| 27 | Fake optimization criteria | -2 |
| 28 | Entangled truths | ±3 |
| 29 | Cached thought | ±2 |
| 30 | Absence of expected evidence | -3 |

12 critères sont **core** (toujours évalués) : #1, #2, #3, #4, #5, #8, #14,
#23, #24, #25, #28, #30. Les autres sont toujours évalués, mais peuvent recevoir
n/a s’ils ne s’appliquent pas au type de message.

### 4. Sortie en 3 niveaux

**Niveau 1** — Le message + Score + tier prédit
```
## Ton message (Score: 18 · REPLY_NEEDED 🔴)

[Texte du brouillon]
```

**Niveau 2** — Les 3 principaux points forts et points faibles, avec des suggestions d’amélioration
```
## Points forts
+5  #1  Change quelque chose de concret — tu demandes une revue de la conception avant jeudi
+4  #24 Hug the query — tu vas directement à la décision d’approuver ou d’itérer

## Points faibles
-2  #11 Distance inférentielle — tu supposes que le schéma v3 est connu
         → Ajouter une ligne de contexte
```

**Niveau 3** — Détail complet des 30 critères (une ligne par critère)

### 5. Itération par la conversation

Après le diagnostic, tu itères en discutant — sans invoquer de nouveau le skill :
- « Réécris-le plus directement »
- « Améliore le deuxième paragraphe »
- « Pourquoi le Score est-il de -2 pour la distance inférentielle ? »
- « Quel Score aurait-il si je supprimais cette phrase ? »
- « Et si je l’envoyais à une autre personne ? »

### Tiers de prédiction

| Tier | Score | Signification |
|------|-------|-------------|
| REPLY_NEEDED 🔴 | ≥ 10 | Ton message susciterait une réponse active |
| REVIEW 🟡 | 4–9 | Ton message serait lu avec attention |
| READING_LATER 🔵 | 0–3 | Ton message serait lu « quand je pourrai » |
| ARCHIVE ⚪ | < 0 | Ton message serait ignoré ou archivé |

## Modes d’entrée

| Mode | Quand | Ce qu’il fait |
|------|--------|----------|
| **Composition** | Tu veux rédiger un nouveau message | Entretien complet → brouillon → diagnostic |
| **Évaluation** | Tu as déjà un brouillon | Passe l’entretien sur le contenu et évalue directement |
| **Réponse** | Tu veux répondre à un message reçu | Entretien adapté au contexte du fil de discussion |

## Langues

Le skill fonctionne en espagnol (`es`), en anglais (`en`) et en français (`fr`). Par défaut,
`usuario.idioma` dans `config.yaml` est défini sur `"auto"` : il utilise la langue du
premier message de l’utilisateur et, s’il ne peut pas la déterminer, l’espagnol.

Pour imposer une langue, remplace `idioma: "auto"` par `idioma: "es"`,
`idioma: "en"` ou `idioma: "fr"` dans `usuario` dans `config.yaml`. Le brouillon peut utiliser
une autre langue si tu la précises pour le destinataire.

En français, le skill s’active selon le sens de la demande, avec
"bayesian compose" ou avec `/bayesian-compose`.

## Installation

### Depuis Cowork (recommandé)

1. Ouvre **Personnaliser** → **Plugins**
2. Clique sur **Ajouter un marketplace**
3. Colle : `novanoticia/bayesian-compose-plugin`
4. Clique sur **Synchroniser**
5. Active le plugin **bayesian-compose** avec le bouton "+"

### Depuis Claude Code (CLI)

1. Ouvre Claude Code
2. Va dans **Settings** → **Plugins** → **Add Marketplace**
3. Ajoute : `novanoticia/bayesian-compose-plugin`
4. Active le plugin

### Depuis Claude Chat (Skills)

1. Télécharge le paquet [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/releases/latest/download/bayesian-compose.zip) (section **Releases** du dépôt).
2. Dans Claude Chat, va dans **Skills** → **Importer** et importe le `.zip`.
3. Active le skill **bayesian-compose** dans ta conversation.

### Depuis Perplexity (Skills)

1. Télécharge le paquet [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/releases/latest/download/bayesian-compose.zip) (section **Releases** du dépôt).
2. Dans Perplexity, va dans **Skills** → **Téléverser/Importer un skill** et sélectionne le `.zip`.

> **Note technique :** la limite de longueur du champ `description` dépend de la plateforme : Perplexity vérifie les **octets UTF-8** (limite de 1024) et Mistral les **caractères** (limite de 500). La description de ce skill mesure **434 caractères / 446 octets**, dans les deux limites. Si tu la modifies, ne dépasse pas **500 caractères** pour conserver la compatibilité avec Mistral.

### Depuis Mistral AI (Skills)

1. Télécharge le paquet [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/releases/latest/download/bayesian-compose.zip) (section **Releases** du dépôt) et **décompresse-le**.
2. Dans Mistral AI, au sein de l’espace **Work**, ouvre **Skills** et sélectionne le **dossier** obtenu (`bayesian-compose/`, celui qui contient `SKILL.md`).

### Vérifier l’installation

Après l’installation, commence une nouvelle conversation et écris :
```
/bayesian-compose
```

Claude devrait commencer l’entretien socratique.

## Configuration

Modifie `skills/bayesian-compose/config.yaml` pour personnaliser :

### Profil utilisateur
```yaml
usuario:
  nombre: "Ton nom"
  perfil: "Ton rôle, ta formation et tes centres d’intérêt"
  idioma: "es"
```

### Type de message
```yaml
mensaje:
  tipo_default: "email"      # email, slack, whatsapp, carta, general
  tono_default: "profesional" # professionnel, informel, formel, direct, empathique
  incluir_saludo: true
  incluir_despedida: true
```

### Entretien
```yaml
entrevista:
  pregunta_6_auto: true   # Claude décide s’il faut poser la question 6
  gate_estricto: true      # La question 1 bloque s’il n’y a pas d’action concrète
```

### Sortie
```yaml
output:
  mostrar_nivel_1: true    # Message + Score
  mostrar_nivel_2: true    # Points forts et points faibles
  mostrar_nivel_3: true    # Détail complet des 30 critères
  razones_positivas: 3
  razones_negativas: 3
```

### Tiers (seuils)
```yaml
tiers:
  reply_needed: 10
  review: 4
  reading_later: 0
  archive: -1
```

### Critères épistémiques
Chaque critère peut être désactivé ou ajusté individuellement :
```yaml
criterios_epistemicos:
  cambia_algo_concreto:
    activo: true
    core: true
    weight: 5
    question: "Mon message contient-il une action ou un changement concret ?"
```

### Télémétrie (facultative)
Pour enregistrer des sessions et repérer des tendances dans ta rédaction :
```bash
mkdir -p ~/.bayesian-compose
```
Le skill écrit uniquement si le dossier existe. Il ne le crée pas automatiquement.

## Exemple d’utilisation

**Invocation :**
```
/bayesian-compose
```

**Question 1 (gate) :**
> Que veux-tu que le destinataire FASSE après avoir lu ton message ?

**Ta réponse :**
> Qu’il examine la conception du tableau de bord avant jeudi et me dise s’il l’approuve
> ou s’il souhaite itérer.

**Question 2 :**
> Quelle est la décision réelle que ce message concerne ?

**Ta réponse :**
> Si nous lançons le tableau de bord avec la conception actuelle ou si nous faisons une nouvelle itération.

*(...questions 3-5...)*

**Sortie :**
```
## Ton message (Score: 22 · REPLY_NEEDED 🔴)

María,

La conception du tableau de bord pour le lancement de vendredi est finalisée
depuis hier. J’ai besoin de ton approbation avant jeudi à 14:00 pour
que l’équipe front puisse l’intégrer.

Les données : le test d’utilisabilité avec 12 utilisateurs a donné un SUS de 78
(au-dessus du seuil de 68). Le seul point faible était la navigation
du filtre de dates — je l’ai documenté dans DESIGN-847.

Options : (a) tu approuves en l’état, (b) nous itérons sur le filtre de dates
et déplaçons le lancement à lundi, (c) nous lançons sans le filtre et
l’améliorons en v1.1.

15 min demain pour décider ?

## Points forts
+5  #1  Change quelque chose de concret — approbation ou itération avec une échéance
+4  #24 Hug the query — directement à la décision de lancer/d’itérer
+3  #28 Entangled truths — SUS 78, 12 utilisateurs, ticket DESIGN-847, date

## Points faibles
 0  #7  Confusion productive — aucun écart surprenant ici
 0  #15 Pertinence à long terme — décision tactique, pas stratégique
+1  #29 Cached thought — la conclusion « 15 min ? » est une formule un peu toute faite
         → Proposer un créneau précis : « demain à 10:30 ou à 16:00 ? »
```

## Dépannage

### Le skill n’apparaît pas après l’installation
Ferme et rouvre Claude Code/Cowork. Les skills sont chargés au début de la session.

### « marketplace.json introuvable »
Assure-toi d’ajouter `novanoticia/bayesian-compose-plugin` (sans `https://github.com/`).

### Le gate de la question 1 est trop strict
Passe à `entrevista.gate_estricto: false` dans `config.yaml`. Claude avertira
mais ne bloquera pas.

### Je veux voir uniquement le Score, pas le détail complet
Passe à `output.mostrar_nivel_3: false` dans `config.yaml`.

### Les Scores semblent faibles pour des messages que je trouve bons
Les Scores sont calculés depuis la perspective du **destinataire**, pas la tienne. Un message
qui te semble précieux peut l’être moins pour le destinataire s’il connaît déjà
l’information, s’il n’y a pas d’action concrète ou si l’urgence
est davantage la tienne que la sienne.

## Scores de référence

| Plage | Interprétation |
|-------|----------------|
| 25-55 | Exceptionnel — message à fort impact épistémique |
| 15-24 | Bon — message clair, permettant d’agir, bien étayé |
| 5-14 | Acceptable — satisfait aux exigences mais peut être amélioré |
| 0-4 | Faible — le destinataire remettrait probablement sa lecture à plus tard |
| < 0 | Le message ne devrait probablement pas être envoyé sous cette forme |

Score maximal théorique : +55. Score minimal théorique : -62.

## Crédits

Conçu par Pablo Rodríguez López ([mindandhealth.org](https://mindandhealth.org/))
avec l’assistance de Claude et de **Vibe Code** (coauteur des implémentations de compatibilité).

Avec la collaboration de [**Codex d’OpenAI (ChatGPT)**](https://github.com/codex).

Critères épistémiques fondés sur les [Sequences](https://www.lesswrong.com/rationality)
d’Eliezer Yudkowsky (LessWrong).

Icône générée avec ChatGPT (image créée par IA).

## Confidentialité

Le plugin n’envoie aucune donnée hors de la plateforme et ne conserve rien par défaut. Détails dans la [politique de confidentialité (Privacy)](./PRIVACY.md).

## Licence

Apache 2.0 — voir [LICENSE](./LICENSE).

## Liens

- [Dépôt sur GitHub](https://github.com/novanoticia/bayesian-compose-plugin)
- [Issues](https://github.com/novanoticia/bayesian-compose-plugin/issues)
- [Plugin complémentaire : Email Triage](https://github.com/novanoticia/email-triage-plugin)
