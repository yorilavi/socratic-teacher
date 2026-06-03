# Changelog

All notable changes to the **socratic-teacher** skill are recorded here.
Format loosely follows [Keep a Changelog](https://keepachangelog.com/). Dates are absolute (YYYY-MM-DD).

## 2026-06-03 — Generic framework backport (`SKILL.md`)

Backported three improvements from the Graph RAG **V6** instance into the universal framework, generalized past Graph RAG. These came from observed behavior while running the skill live, not speculative review.

### Added
- **Spine concepts.** New framework section plus Construction step (E): identify 1–2 recurring tradeoffs/invariants up front and make the learner *recognize* later instances instead of re-deriving them.
- **Clarify-don't-diagnose branch.** The response cycle now classifies the learner's message first; clarification/meta-questions get a plain answer plus a re-posed question, not a full diagnose/teach/deepen cycle. Matching anti-pattern and stuck-protocol carve-out added.
- `CHANGELOG.md` (this file) and `.gitignore` (excludes `.DS_Store`).

### Changed
- **Synthesis cadence enforced.** Replaced the soft "at least once every 5 cycles" with a tracked counter and a hard obligation at cycles 5 / 10 / 15…
- **Provenance** now cites both V5 (baseline) and V6 (current) instances and points here.

> Note: the **session-end protocol** — the fourth V6 improvement — already existed in `SKILL.md`, so it was not re-added.

## 2026-06-03 — `graph-rag-socratic-v6.md`

New Graph RAG instance built from a full live run of V5. **V5 is left unchanged as the canonical baseline.**

### Added (over V5)
- Spine concepts (the recall/precision tension reused across top-k → traversal fan-out → entity-resolution blocking).
- Synthesis enforcement (tracked counter at cycles 5 / 10 / 15).
- Clarify-don't-diagnose branch in the response cycle.
- Session-end protocol (confirm → consolidate → flag light-coverage scope → stop).
- Sharpened payback framing (entity/relationship density gates *constructibility*; multi-hop frequency × value × vector-unanswerability gates *profitability*) and a pre-build validation step in the completion criterion.

## 2026-06-03 — Initial repository

- `git init` in the skill folder as a **standalone repo** (intentionally not nested under `~/.claude`); first commit covers `SKILL.md`, both Graph RAG instances, and the prompt-evolution log.
- Pushed to https://github.com/yorilavi/socratic-teacher (public).

## ~2026-05-15 — Prompt optimization (pre-git)

Full detail in `prompt-evolution-20260515-132231.md`.

- **V1:** one-line request to learn Graph RAG Socratically.
- **V2–V5:** iterated via the Prompt Optimizer skill — 1 initial Claude pass + 3 GPT review passes, each Claude-critiqued. Added across rounds: explicit Socratic mechanics, the diagnose → teach → deepen cycle, predict-from-primitives anchoring, an operationalized "structural limitation" definition, verbosity caps, graduated stall recovery, graph sub-typing, an instruction-conflict priority hierarchy, factual discipline, and a transfer-testing completion criterion.
- **V5** declared the diminishing-returns stopping point (substantive changes per round: 5 → 5 → 2).
- Productized into `SKILL.md` — the generic framework with Discovery / Construction / Teach phases.
