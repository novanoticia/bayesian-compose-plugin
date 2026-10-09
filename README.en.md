🇪🇸 [Versión en español](README.md) · 🇫🇷 [Version française](README.fr.md)

# Bayesian Compose v1.3.0

Epistemic message composition for Claude Cowork and Claude Code.

> **Compatible with [Agent Plugins 1.0.0](https://agent-plugins.org/specification)** — the portable packaging format from the Agentic AI Foundation (OpenAI, Amazon,
> Microsoft, Cursor and Vercel, with Google as a *core maintainer*).
> The package includes the portable `plugin.json` manifest at the plugin root and
> the skill at `plugins/bayesian-compose/skills/bayesian-compose/SKILL.md`, so any conforming client can discover it.
>
> **Works in ChatGPT.** The skill is text: instructions and criteria, with no
> local execution, so you install it by enabling **Work** in ChatGPT's selector and
> adding it from **Plugins**, by name or by this repository's URL.
> It works the same way as in Claude. Its frontmatter
> validates against the closed set of fields in [Agent Skills](https://agentskills.io/specification),
> which ChatGPT, claude.ai and the Skills API require to accept an upload
> — an extra key is not ignored; it causes a hard error. They are also available on the
> **free plan**, with usage limits.

## What it does

It interviews you before writing any message (email, Slack, WhatsApp, letter,
any text) to maximize its epistemic quality. It evaluates the resulting draft
against 30 Bayesian rationality criteria (LessWrong Sequences) from the
**recipient's estimated perspective** — not yours.

It is not an email rewriter. It is an exercise in **epistemic empathy**: it makes
you think from the other side before writing.

## Philosophy

Most writing tools ask "does it sound good?". This plugin
asks something different:

- Does it change something concrete for the recipient? (Value of Information)
- Am I telling them something they did not expect? (Bayesian Surprise)
- Am I including all the evidence, or only what favors me? (Filtered Evidence)
- Am I really exploring, or seeking validation? (Forward vs Backward Flow)
- Is the urgency real or manufactured? (Real vs Manufactured Urgency)
- Is it anchored to verifiable facts? (Entangled Truths)
- Did I decide first and reason afterward? (Fake Justification)
- Is there something uncomfortable I am leaving out? (Absence of Expected Evidence)

The result is not a pretty text, but a message that **deserves the recipient's
attention** — measured with the same 30 criteria that the
[email-triage](https://github.com/novanoticia/email-triage-plugin) plugin uses to
filter incoming mail.

## Relationship with Email Triage

They are two sides of the same epistemic coin:

| | Email Triage | Bayesian Compose |
|---|---|---|
| **Direction** | Messages you receive | Messages you send |
| **Question** | "Does it deserve my attention?" | "Does it deserve the recipient's attention?" |
| **Criteria** | 30 (Bayesian rationality) | The same 30, reversed for sending |
| **Perspective** | Yours (recipient) | The other person's (estimated recipient) |

They are independent tools. Neither requires the other to be installed. But
if both are active, they form a two-way system: you filter what you receive
with epistemic rigor and send with the same rigor.

## How it works

### 1. Socratic interview (5+1 questions)

Before writing anything, the skill asks you questions that map to the most
important epistemic criteria:

| # | Question | What it assesses |
|---|----------|------------|
| 1 | **What do you want the recipient to DO?** | Whether there is a concrete action (GATE: if there is none, the message perhaps should not exist) |
| 2 | **What is the actual decision being addressed?** | Whether you are addressing the decision or talking around it |
| 3 | **What verifiable facts support this?** | Whether there are verifiable anchors (dates, metrics, tickets) |
| 4 | **Is there anything you should include but would rather leave out?** | Whether you are filtering evidence (the most important question) |
| 5 | **What happens if they read it tomorrow instead of now?** | Whether the urgency is real or manufactured |
| 6 | **Who is receiving this, and what do they already know?** | Inferential distance and calibration to the recipient (optional) |

**Question 1 is a gate**: if there is no concrete action, the skill offers you
the choice to rethink, continue with an expected low score, or wait to send it.

### 2. Guided draft

Using your answers, Claude generates a draft that:
- Opens with the action/decision (not context)
- Anchors its claims to verifiable facts
- Includes the uncomfortable information, if any
- Calibrates complexity to the recipient
- Does not use jargon that shuts down thought

The draft is a **guide, not a final text**. It rewrites it on request.

### 3. Diagnosis against 30 criteria

It evaluates the draft against all 30 criteria, every time, grouped into 4 axes:

**Group A — Value of information**
| # | Criterion | Weight |
|---|----------|------|
| 1 | Changes something concrete | ±5 |

**Group B — Bayesian updating**
| # | Criterion | Weight |
|---|----------|------|
| 2 | Change in predictions | ±4 |
| 3 | Bayesian surprise | ±3 |
| 4 | Filtered evidence | -3 |
| 5 | Forward/Backward flow | ±3 |

**Group C — Attention design and usefulness**
| # | Criterion | Weight |
|---|----------|------|
| 6 | Return on attention | ±2 |
| 7 | Productive confusion | +4 |
| 8 | Real causal impact | +4 |
| 9 | Social noise | -3 |
| 10 | Opens up options | +3 |
| 11 | Inferential distance | -2 |
| 12 | Strategic agent | -3 |
| 13 | Information density | ±2 |
| 14 | Real vs manufactured urgency | ±3 |
| 15 | Long-term relevance | +4 |

**Group D — Countering bias and argument quality**
| # | Criterion | Weight |
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

12 criteria are **core** (always assessed): #1, #2, #3, #4, #5, #8, #14,
#23, #24, #25, #28, #30. The rest are always assessed but can be scored
n/a if they do not apply to the type of message.

### 4. Output at 3 levels

**Level 1** — The message + score + predicted tier
```
## Your message (Score: 18 · REPLY_NEEDED 🔴)

[Draft text]
```

**Level 2** — Top 3 strengths and weaknesses with suggestions for improvement
```
## Strengths
+5  #1  Changes something concrete — you request a design review before Thursday
+4  #24 Hug the query — straight to the decision to approve or iterate

## Weaknesses
-2  #11 Inferential distance — you assume knowledge of schema v3
         → Add a line of context
```

**Level 3** — Full breakdown of the 30 criteria (one line each)

### 5. Iteration through conversation

After the diagnosis, you iterate through conversation — without invoking the skill again:
- "Rewrite it more directly"
- "Improve the second paragraph"
- "Why does it score -2 on inferential distance?"
- "What score would it have if I remove this sentence?"
- "What if I send it to someone else?"

### Prediction tiers

| Tier | Score | Meaning |
|------|-------|-------------|
| REPLY_NEEDED 🔴 | ≥ 10 | Your message would prompt an active response |
| REVIEW 🟡 | 4–9 | Your message would be read attentively |
| READING_LATER 🔵 | 0–3 | Your message would be read "when I can" |
| ARCHIVE ⚪ | < 0 | Your message would be ignored or archived |

## Input modes

| Mode | When | What it does |
|------|--------|----------|
| **Composition** | You want to write a new message | Full interview → draft → diagnosis |
| **Evaluation** | You already have a draft | Skips the content interview, evaluates directly |
| **Reply** | You want to reply to a received message | Interview adapted to the thread context |

## Languages

The skill works in Spanish (`es`), English (`en`) and French (`fr`). By default,
`usuario.idioma` in `config.yaml` is set to `"auto"`: it uses the language of
the user's first message and, if it cannot determine it, Spanish.

To force a language, replace `idioma: "auto"` with `idioma: "es"` or
`idioma: "en"` or `idioma: "fr"` under `usuario` in `config.yaml`. The draft can use another
language if you specify it for the recipient.

In French, the skill activates based on the meaning of the request, with
"bayesian compose" or with `/bayesian-compose`.

## Installation

### From Cowork (recommended)

1. Open **Customize** → **Plugins**
2. Click **Add marketplace**
3. Paste: `novanoticia/bayesian-compose-plugin`
4. Click **Sync**
5. Enable the **bayesian-compose** plugin with the "+" button

### From Claude Code (CLI)

1. Open Claude Code
2. Go to **Settings** → **Plugins** → **Add Marketplace**
3. Add: `novanoticia/bayesian-compose-plugin`
4. Enable the plugin

### From Claude Chat (Skills)

1. Download the [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/releases/latest/download/bayesian-compose.zip) package (the repository's **Releases** section).
2. In Claude Chat, go to **Skills** → **Import** and upload the `.zip`.
3. Enable the **bayesian-compose** skill in your conversation.

### From Perplexity (Skills)

1. Download the [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/releases/latest/download/bayesian-compose.zip) package (the repository's **Releases** section).
2. In Perplexity, go to **Skills** → **Upload/Import skill** and select the `.zip`.

> **Technical note:** the length limit for the `description` field depends on the platform: Perplexity validates **UTF-8 bytes** (limit 1024), and Mistral validates **characters** (limit 500). This skill's description is **434 characters / 446 bytes**, within both limits. If you edit it, do not exceed **500 characters** to retain compatibility with Mistral.

### From Mistral AI (Skills)

1. Download the [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/releases/latest/download/bayesian-compose.zip) package (the repository's **Releases** section) and **unzip it**.
2. In Mistral AI, within the **Work** space, open **Skills** and select the resulting **folder** (`bayesian-compose/`, the one containing `SKILL.md`).

### Verify installation

After installing, start a new conversation and type:
```
/bayesian-compose
```

Claude should start the Socratic interview.

## Configuration

Your personal configuration lives in **`~/.bayesian-compose/config.yaml`**,
outside the plugin: it is editable and survives updates. The `config.yaml`
shipped in the package is a template only.

You can create or change it from the conversation:

> Bayesian Compose, create my personal configuration.
> Bayesian Compose, save a direct tone as my default.
> Bayesian Compose, save that I do not want the full criteria breakdown.

The assistant copies the full template if you do not have a personal config,
changes only what you request and creates a backup before modifying an
existing file. You can also edit the copy with your text editor.

In Cowork, grant access to the folder on your computer containing the copy.
If your client uses another writable, persistent location, tell the assistant;
you can set `BAYESIAN_COMPOSE_HOME` to that directory in environments with
environment variables. The file is named `config.yaml`, and the assistant
will tell you which path it is using.

Without file access, attach or paste your `config.yaml`: the assistant returns
the updated YAML for you to save and attach in future conversations.

If you previously customized the YAML inside the plugin, copy **that file**
to the personal location before updating. An existing personal config is
never replaced with a new template.

These are the sections you can customize in your copy:

### User profile
```yaml
usuario:
  nombre: "Your name"
  perfil: "Your role, background and interests"
  idioma: "es"
```

### Message type
```yaml
mensaje:
  tipo_default: "email"      # email, slack, whatsapp, carta, general
  tono_default: "profesional" # profesional, informal, formal, directo, empático
  incluir_saludo: true
  incluir_despedida: true
```

### Interview
```yaml
entrevista:
  pregunta_6_auto: true   # Claude decides whether to ask question 6
  gate_estricto: true      # Question 1 blocks progress if there is no concrete action
```

### Output
```yaml
output:
  mostrar_nivel_1: true    # Message + score
  mostrar_nivel_2: true    # Strengths and weaknesses
  mostrar_nivel_3: true    # Full breakdown of 30 criteria
  razones_positivas: 3
  razones_negativas: 3
```

### Tiers (thresholds)
```yaml
tiers:
  reply_needed: 10
  review: 4
  reading_later: 0
  archive: -1
```

### Epistemic criteria
Each criterion can be individually disabled or adjusted:
```yaml
criterios_epistemicos:
  cambia_algo_concreto:
    activo: true
    core: true
    weight: 5
    question: "Does my message contain a concrete action or change?"
```

### Telemetry (optional)
To record sessions and identify patterns in your writing, ask the assistant
to enable telemetry and create the directory if it does not exist:
```bash
mkdir -p ~/.bayesian-compose
```
The skill records only when you explicitly request it and the directory exists.
Creating the personal configuration does not enable telemetry.

## Usage example

**Invocation:**
```
/bayesian-compose
```

**Question 1 (gate):**
> What do you want the recipient to DO after reading your message?

**Your answer:**
> To review the dashboard design before Thursday and tell me whether they approve
> or want to iterate.

**Question 2:**
> What is the actual decision this message addresses?

**Your answer:**
> Whether we launch the dashboard with the current design or do one more round.

*(...questions 3-5...)*

**Output:**
```
## Your message (Score: 22 · REPLY_NEEDED 🔴)

María,

The dashboard for Friday's launch has had its design finalized
since yesterday. I need your approval before Thursday at 14:00 so
that the front-end team can integrate it.

The data: the usability test with 12 users produced a SUS of 78
(above the threshold of 68). The only weak point was navigation
in the date filter — I documented it in DESIGN-847.

Options: (a) approve as is, (b) iterate on the date filter
and move the launch to Monday, (c) launch without the filter and
improve it in v1.1.

15 min tomorrow to decide?

## Strengths
+5  #1  Changes something concrete — approval or iteration with a deadline
+4  #24 Hug the query — straight to the launch/iterate decision
+3  #28 Entangled truths — SUS 78, 12 users, ticket DESIGN-847, date

## Weaknesses
 0  #7  Productive confusion — no surprising gap here
 0  #15 Long-term relevance — tactical decision, not strategic
+1  #29 Cached thought — the closing "15 min?" is somewhat canned
         → Suggest a specific slot: "tomorrow at 10:30 or 16:00?"
```

## Troubleshooting

### The skill does not appear after installation
Close and reopen Claude Code/Cowork. Skills are loaded at the start of a session.

### "marketplace.json not found"
Make sure you add `novanoticia/bayesian-compose-plugin` (without `https://github.com/`).

### The gate in question 1 is too strict
Change `entrevista.gate_estricto: false` in `config.yaml`. Claude will warn
but will not block progress.

### I want to see only the score, not the full breakdown
Change `output.mostrar_nivel_3: false` in `config.yaml`.

### Scores seem low for messages I think are good
Scores are from the **recipient's** perspective, not yours. A message
that seems valuable to you may be less valuable to the recipient if they already
know the information, if it has no concrete action, or if the urgency is
more yours than theirs.

## Reference scores

| Range | Interpretation |
|-------|----------------|
| 25-55 | Exceptional — a message with high epistemic impact |
| 15-24 | Good — a clear, actionable, well-supported message |
| 5-14 | Acceptable — meets the requirements but has room for improvement |
| 0-4 | Low — the recipient would probably postpone reading it |
| < 0 | The message probably should not be sent in this form |

Theoretical maximum score: +55. Theoretical minimum score: -62.

## Credits

Designed by Pablo Rodríguez López ([mindandhealth.org](https://mindandhealth.org/))
with assistance from Claude and **Vibe Code** (co-author of compatibility implementations).

With contributions from [**OpenAI Codex (ChatGPT)**](https://github.com/codex).

Epistemic criteria based on the [Sequences](https://www.lesswrong.com/rationality)
by Eliezer Yudkowsky (LessWrong).

Icon generated with ChatGPT (AI-created image).

## Privacy

The plugin does not send data outside the platform or store anything by default. Details in the [privacy policy (Privacy)](./PRIVACY.md).

## License

Apache 2.0 — see [LICENSE](./LICENSE).

## Links

- [GitHub repository](https://github.com/novanoticia/bayesian-compose-plugin)
- [Issues](https://github.com/novanoticia/bayesian-compose-plugin/issues)
- [Companion plugin: Email Triage](https://github.com/novanoticia/email-triage-plugin)
