# socratic-teacher

A Claude Code skill that teaches a domain through rigorous Socratic dialogue — deep questions instead of lecture — by anchoring every new idea to expertise the learner already has.

---

## The idea

Most "teach me X" sessions with an LLM collapse into a lecture with occasional rhetorical questions. You read, you nod, and almost none of it survives the week, because recognition is not understanding. You can recognize a definition you were just handed without being able to *predict* what the thing does, or *decide* with it under pressure.

This skill refuses to lecture. It runs a disciplined loop — **diagnose → teach → deepen** — where every concept is something the learner is made to *predict from primitives they already command* before it's ever explained. The teaching happens in the gap between their prediction and what actually happens. New knowledge gets bolted onto load-bearing structure instead of floating free.

The session is built in three phases:

```
Discovery     ─►  gather domain, the learner's real adjacent expertise,
                  a completion criterion, and format constraints
                     │
                     ▼
Construction  ─►  (internal) curriculum in dependency order, operational
                  targets for pivotal concepts, spine concepts, the first move
                     │
                     ▼
Teach         ─►  run the universal framework: one question at a time,
                  predict-before-explain, pressure shallow answers,
                  enforced synthesis, stop at the completion criterion
```

## Why this works (and why a lecture doesn't)

The lever is **prediction under your own existing model.** When you're asked to predict how a graph traversal behaves *using your SQL-join intuition* before anyone defines graph traversal, one of two things happens: you get it right and the new concept is now anchored to something durable, or you get it wrong and the correction lands exactly where your mental model was broken. Either way the knowledge has somewhere to live. A lecture skips this step entirely — it hands you the answer before you've felt the question, so there's no gap for understanding to fill.

Three design choices make that loop bite instead of drift:

1. **Operational targets, not vibes.** For each pivotal concept, Construction defines what counts as a *real* answer versus a *surface* one — an explicit rejection list. Without it, the model accepts the first plausible-sounding answer and the learner walks away with fluency they don't have. With it, the dialogue keeps pressing until the learner names something structural.

2. **Spine concepts.** A domain's hardest tradeoffs recur in different costumes (in Graph RAG, the recall/precision tension reappears at top-k retrieval, traversal fan-out, and entity-resolution blocking). Naming the spine once lets the session make the learner *recognize* later instances rather than re-derive them — which is exactly the move that turns isolated facts into a connected model.

3. **Enforced synthesis.** At fixed cadence (cycles 5 / 10 / 15…) the session must ask a question that fuses two earlier concepts. This is the difference between a pile of correct answers and an integrated model you can actually reason with.

The trap to avoid: treating the question-asking as the point. It isn't. The questions are scaffolding for prediction. When a learner says "just tell me," the skill respects it and switches to direct teaching with check-ins — the method is a default, not a cage.

## Install

Pick whichever path fits how you got here.

**1. Direct `git clone` — the recommended path.** Same command works as install and as update (just `git pull` later). A clone also brings the Graph RAG example instances, not just the framework.

```sh
# macOS / Linux / WSL / Git Bash on Windows
git clone https://github.com/yorilavi/socratic-teacher.git ~/.claude/skills/socratic-teacher
```

```powershell
# Windows PowerShell
git clone https://github.com/yorilavi/socratic-teacher.git "$env:USERPROFILE\.claude\skills\socratic-teacher"
```

**2. Install script — single entry point for install, fresh clone, or update.** Auto-detects which mode is right based on what's already on disk. Works from an unzipped folder, from a forwarded copy of the script alone, or from a previous install.

```sh
sh install.sh                                                # macOS / Linux / WSL / Git Bash
powershell -ExecutionPolicy Bypass -File .\install.ps1       # Windows
```

**3. One-line remote install** — pipes the script straight from GitHub. Convenient, but `curl | sh` is a trust call you should make consciously; read the script first if you're unsure.

```sh
curl -fsSL https://raw.githubusercontent.com/yorilavi/socratic-teacher/main/install.sh | sh
```

```powershell
iwr -useb https://raw.githubusercontent.com/yorilavi/socratic-teacher/main/install.ps1 | iex
```

Restart Claude Code. Verify it loaded with `/skills` — you should see `socratic-teacher` in the list.

**Updating later:** re-run `install.sh` (it'll detect the existing checkout and `git pull`), or `cd ~/.claude/skills/socratic-teacher && git pull` directly.

Detailed install + troubleshooting + uninstall: see [INSTALL.md](./INSTALL.md).

## Usage

In any Claude Code session:

```
/socratic-teacher
```

Or describe what you want:

> "Teach me Graph RAG socratically — I already know vector search and SQL joins."

The skill opens with **Discovery**: four questions in one message you can answer all at once.

1. **Domain** — what specifically you want to learn (one topic, not a survey).
2. **Background** — the adjacent concepts, tools, and experience your new knowledge will be anchored to. Specifics matter; "I'm a programmer" gets pushed for detail.
3. **Completion criterion** — what you should be able to answer, decide, or do when you're done. This becomes the test that ends the session.
4. **Format preferences** — any constraints (short questions, code examples, no analogies, a time box).

Then it builds the curriculum internally and starts teaching — beginning not with a definition but with a concrete scenario where your *existing* toolkit fails in a way the new domain would solve.

## What ships in this repo

- **`SKILL.md`** — the universal teaching framework. This is the skill.
- **`graph-rag-socratic-v5.md` / `graph-rag-socratic-v6.md`** — worked Graph RAG instances; the canonical examples and the authority if an instance ever behaves inconsistently with the framework.
- **`prompt-evolution-20260515-132231.md`** — the optimization log the framework was distilled from.
- **`CHANGELOG.md`** — version history.

## Requirements

- **Claude Code** — CLI, VS Code extension, or JetBrains plugin. Nothing else.

## Updates

Re-run the install script (it'll detect the existing checkout and pull):

```sh
sh install.sh
```

…or update directly with git:

```sh
cd ~/.claude/skills/socratic-teacher && git pull
```

Subscribe to releases at the [repo page](https://github.com/yorilavi/socratic-teacher) for change notifications. See [CHANGELOG.md](./CHANGELOG.md) for the version history.

## License

[MIT](./LICENSE). Attribution appreciated but not required.

## Author

**Yori Lavi** · current version: **v1.0.1**

Issues and suggestions: open one on the [repo](https://github.com/yorilavi/socratic-teacher/issues), or DM me directly if you got this skill from me.
