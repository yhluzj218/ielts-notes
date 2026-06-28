# DECISIONS — Architecture Decision Log

Decisions are recorded in reverse-chronological order. Each entry answers: what, why, and what was rejected.

---

## ADR-001 — Use this repository as the single source of truth

**Date:** 2026-06-28
**Status:** Accepted

**Decision:** The coach reads Markdown files in this repo as its knowledge base. No external database, vector store, or CMS in MVP.

**Why:** The notes are already here, structured, and git-versioned. Adding a database layer in MVP would be premature — the bottleneck is grading quality, not retrieval speed.

**Rejected alternatives:**
- Notion as knowledge base: loses git history and Claude Code integration
- Vector embedding store: overkill for a single-user, single-exam knowledge base of < 50 files

---

## ADR-002 — Claude Code (CLAUDE.md) as the primary coach runtime

**Date:** 2026-06-28
**Status:** Accepted

**Decision:** Coach behaviours (grading, model generation, notes update, Anki) are defined as natural-language instructions in `CLAUDE.md`. No custom application code in MVP.

**Why:** The existing CLAUDE.md workflow already works end-to-end. Rewriting it as code before validating the feedback quality is waste.

**Rejected alternatives:**
- Python CLI wrapper: adds dev overhead before the product is validated
- Web app with API: far too early; no multi-user requirement

**Review trigger:** When file count exceeds ~200 or response latency becomes painful, reconsider moving to a proper retrieval + API architecture.

---

## ADR-003 — Separate teacher profiles into 08_ai/teachers/

**Date:** 2026-06-28
**Status:** Accepted

**Decision:** Each teacher gets their own profile file under `08_ai/teachers/` (e.g. `matt.md`, `joe.md`). The coach loads the relevant profile before grading.

**Why:** `01_lessons/teacher.md` mixes both teachers' principles. Separating them lets the coach load only the relevant context per task (writing → Matt, speaking → Joe), reducing prompt length and avoiding cross-contamination.

**Rejected alternatives:**
- Keep one combined `teacher.md`: works now, but will become unmanageable as notes grow
- Embed teacher style inline in CLAUDE.md: makes CLAUDE.md hard to maintain

---

## ADR-004 — No vocabulary coaching by default

**Date:** 2026-06-28
**Status:** Accepted

**Decision:** The coach does not recommend vocabulary improvements unless explicitly asked. This is a hard constraint in CLAUDE.md and in teacher profiles.

**Why:** Both Joe and Matt confirmed vocabulary is not my bottleneck. Generic AI tools default to lexical suggestions because they're easy to generate — this coach must not replicate that failure mode.

**How to apply:** Any feedback template that includes a "vocabulary" section must be scoped to collocation errors only, not word-level upgrades.

---

## ADR-005 — Output files are Markdown committed to this repo

**Date:** 2026-06-28
**Status:** Accepted

**Decision:** All coach outputs (feedback, model essays, Anki cards) are `.md` files saved to this repo and committed via git.

**Why:** Markdown is searchable, diffable, and portable. Git provides a history of every grading session. No export step needed.

**Rejected alternatives:**
- PDF export: loses searchability and git diff
- Google Docs: breaks the local-first, offline-capable workflow

---

## ADR-007 — Conflicting teacher opinions: list, don't decide

**Date:** 2026-06-28
**Status:** Accepted

**Decision:** When Joe and Matt give conflicting advice on the same point, the coach lists both positions in a single sentence each and asks Connie to choose. The coach does not pick a side.

**Why:** Joe focuses on speaking, Matt on writing — but their speaking sessions overlapped early on, and future teachers may cover the same ground. Silently prioritising one teacher would hide the conflict and may lead Connie to follow advice she has not consciously chosen.

**How to apply:**
- Sprint Planner: if two teacher profiles give conflicting recommendations, surface the conflict explicitly before proposing a plan.
- Practice Review: if a recurring error has conflicting corrections across teacher notes, show both and ask which to follow.
- Never resolve silently by defaulting to skill-owner (e.g. "writing → Matt wins").

**Rejected alternatives:**
- Skill-owner wins by default (writing → Matt, speaking → Joe): hides cross-skill conflicts and does not work when both teachers commented on the same skill.

---

## ADR-006 — 09_coach/ reserved for future application code

**Date:** 2026-06-28
**Status:** Accepted

**Decision:** `09_coach/` is created now as a clean boundary. No code lives there in MVP. When code becomes necessary (CLI, API, web), it goes here — not mixed into the notes folders.

**Why:** Separating notes from application code from day one prevents folder structure churn when the product grows.
