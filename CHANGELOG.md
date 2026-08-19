# Changelog

All notable changes to the **socratic-teacher** skill are recorded here.
Versioning follows [Semantic Versioning](https://semver.org/):
**MAJOR** = breaking change to the teaching framework · **MINOR** = new capability · **PATCH** = fix or clarification.
Dates are absolute (YYYY-MM-DD).

## Unreleased

### Added
- **`LICENSE`** — MIT. The repo was public with no license, which meant all rights reserved: nobody had the legal right to copy `SKILL.md` into their own `~/.claude/skills/`, which is the one thing the README tells them to do.

### Fixed
- `install.sh`: `mode_local_copy` ended on a bare `[ -f CHANGELOG.md ] && cp …`. Under `set -eu` that made the function return 1 when `CHANGELOG.md` was absent, so the script exited before printing verification or next steps — the install had actually succeeded, but reported as a silent failure with exit 1. Now a full `if`/`fi`.
- `scripts/release.sh`: it rewrote version anchors in `README.md` and `INSTALL.md` unconditionally, so a missing file aborted the run *after* `SKILL.md` had already been modified, leaving the tree half-bumped. Added a preflight that checks all four version-aware files before any edit is applied.
- `install.sh` / `install.ps1`: also copy `LICENSE` into the target in local-copy mode, so a zip install carries the license with it.
- `prompt-evolution-20260515-132231.md`: added a bridging note explaining the Stage 1 → Stage 4 jump (Stages 2–3 were folded into the consolidated V3), so the log reads continuously.

## 1.0.0 — 2026-06-03

Initial public release. The skill is the productized form of an iteratively optimized teaching prompt — a universal Socratic framework with Discovery / Construction / Teach phases, shipped alongside the Graph RAG example instances it was derived from.

### Added
- **`SKILL.md`** — the universal three-phase framework (Discovery, Construction, Teach).
- **Spine concepts.** Framework section plus Construction step (E): identify 1–2 recurring tradeoffs/invariants up front and make the learner *recognize* later instances instead of re-deriving them.
- **Clarify-don't-diagnose branch.** The response cycle classifies the learner's message first; clarification/meta-questions get a plain answer plus a re-posed question, not a full diagnose/teach/deepen cycle. Matching anti-pattern and stuck-protocol carve-out included.
- **Synthesis cadence (enforced).** A tracked counter with a hard obligation at cycles 5 / 10 / 15…, replacing a soft "at least once every 5 cycles".
- **Session-end protocol** — confirm → consolidate → flag light-coverage scope → stop.
- **Graph RAG example instances** — `graph-rag-socratic-v5.md` (the optimization-saturated baseline) and `graph-rag-socratic-v6.md` (improvements observed from a live run, backported into the framework). These are the canonical examples and the authority when an instance behaves inconsistently with the framework.
- **`prompt-evolution-20260515-132231.md`** — the full optimization log.
- Release apparatus: `README.md`, `INSTALL.md`, `install.sh` / `install.ps1`, `scripts/release.sh`, and the `verify-release` GitHub Action.

#### Pre-release history

Development that predates the public release, retained for provenance.

- **~2026-05-15 — Prompt optimization (pre-git).** Full detail in `prompt-evolution-20260515-132231.md`.
  - **V1:** one-line request to learn Graph RAG Socratically.
  - **V2–V5:** iterated via the Prompt Optimizer skill — 1 initial Claude pass + 3 GPT review passes, each Claude-critiqued. Added across rounds: explicit Socratic mechanics, the diagnose → teach → deepen cycle, predict-from-primitives anchoring, an operationalized "structural limitation" definition, verbosity caps, graduated stall recovery, graph sub-typing, an instruction-conflict priority hierarchy, factual discipline, and a transfer-testing completion criterion.
  - **V5** declared the diminishing-returns stopping point (substantive changes per round: 5 → 5 → 2), then was productized into `SKILL.md`.
- **2026-06-03 — `graph-rag-socratic-v6.md`.** New Graph RAG instance built from a full live run of V5 (V5 left unchanged as the canonical baseline). Added over V5: spine concepts, synthesis enforcement, the clarify-don't-diagnose branch, the session-end protocol, and sharpened payback framing with a pre-build validation step.
- **2026-06-03 — Generic framework backport.** Backported the V6 improvements into the universal framework, generalized past Graph RAG. (The session-end protocol already existed in `SKILL.md`, so it was not re-added.)
- **2026-06-03 — Initial repository.** `git init` in the skill folder as a standalone repo; pushed to <https://github.com/yorilavi/socratic-teacher> (public).

### Notes
- Author: Yori Lavi.
- Future improvements should come from observed session failures, not speculative review.
