# Implementation Plan — AI IELTS Coach MVP

> This plan follows the PRD. Any change to scope or phases must be reflected in the PRD first.
>
> **Implementation philosophy:**
> Every interaction improves the Learning Profile.
> Sprint Planning consumes the Learning Profile — it is not the center of the product.

---

## System Model

The Learning Profile is the persistent core. Every capability either writes to it or reads from it.

```
                 ┌─────────────────────────────┐
                 │       Learning Profile       │
                 │  scores · weaknesses ·       │
                 │  mistakes · teacher notes ·  │
                 │  practice history · Sprints  │
                 └──────────┬──────────────────┘
                            │
          writes ───────────┼─────────── reads
             │              │                │
     ┌───────┴──────┐  ┌────┴─────┐  ┌─────┴──────┐
     │   Practice   │  │ Teacher  │  │   Sprint   │
     │   Review     │  │Knowledge │  │  Planner   │
     │ W/S/L/R      │  │Extraction│  │            │
     └──────────────┘  └──────────┘  └────────────┘
             │                              │
             └──────────────────────────────┘
                     Sprint Review
                  (writes back to profile)
```

---

## Phase 1 — Learning Foundation

### Goal

Define the Learning Profile schema and establish the Teacher Personas library — starting with Matt and Joe, extensible to any trusted teacher added over time. Every Phase 2 capability writes to the profile — the schema must be right before any of them run.

### Deliverables

| File | Purpose |
| ---- | ------- |
| `09_coach/connie_profile.md` | Structured profile: current scores, weaknesses by skill, repeated mistakes, study time, practice history, Sprint history |
| `08_ai/teachers/matt.md` | Matt's philosophy and writing methodology, distilled from `01_lessons/writing/` |
| `08_ai/teachers/joe.md` | Joe's philosophy and speaking methodology, distilled from `01_lessons/speaking/` |
| `08_ai/teachers/[name].md` | Any trusted online teacher added in the future — one file per teacher, same schema |

**Format consistency:** Every teacher file uses the same schema (teaching philosophy, skill focus, common feedback patterns, recommended practice methods) so the Sprint Planner can read and compare across teachers uniformly.

**Schema decision required here:** How is the profile structured so that multiple daily interactions can all append to it without conflict? This gates Phase 2.

### Dependencies

- Connie's current IELTS scores (actual or self-assessed) — not yet in any file; needed before building the profile
- Existing notes already readable: `01_lessons/writing/`, `01_lessons/speaking/`, `06_error_database/error_log.md`, `01_lessons/teacher.md`
- No code dependencies

### Complexity

**Low–Medium.** Document work. The risk is getting the schema right on the first attempt.

### Why before Phase 2

Phase 2 capabilities need somewhere consistent to write their output. Without a defined profile schema, each capability invents its own format and nothing accumulates coherently.

---

## Phase 2 — Learning Capabilities

### Goal

Build the capabilities Connie uses daily. After Phase 2, every real interaction — a writing draft, a lesson transcript, a listening result — improves the Learning Profile. Sprint Planning is not required for this phase to be useful.

---

### Capability 2A — Practice Review (Writing / Speaking / Listening / Reading)

**What it does:** Reviews any IELTS practice submission against teacher personas and the official rubric, identifies weaknesses and repeated mistakes, and proposes a Learning Profile update.

| Deliverable | Notes |
| ----------- | ----- |
| `08_ai/templates/practice_review.md` | Review template; final section is always "Profile Updates" — the patterns this session contributes |
| `CLAUDE.md` update | Practice Review instructions per skill type; extend existing `批改` for Writing; add Speaking, Listening, Reading paths; every review ends with a proposed profile update, not just standalone feedback |

Note: the existing `批改` command produces standalone feedback. Phase 2A extends it so the output also proposes a profile update. The feedback format stays; what changes is the final step.

---

### Capability 2B — Teacher Knowledge Extraction

**What it does:** Takes a lesson transcript, extracts new errors, corrections, and principles, appends them to the correct notes files, and proposes a Learning Profile update.

| Deliverable | Notes |
| ----------- | ----- |
| `CLAUDE.md` update | Extend existing `更新筆記` command: after updating `error_log.md`, `teacher.md`, `writing_notes.md`, `speaking_notes.md` — also propose a profile update with the new evidence |

Note: `更新筆記` already exists and works. Phase 2B adds one step at the end.

---

### Capability 2C — Learning Profile Update

**What it does:** The accumulation mechanism. Takes approved evidence from 2A or 2B and appends it to `connie_profile.md` without overwriting history.

| Deliverable | Notes |
| ----------- | ----- |
| `CLAUDE.md` — `更新學習紀錄` command | Appends evidence to profile; includes duplicate check; never overwrites |

This is the connective tissue. Without it, 2A and 2B generate proposals that go nowhere.

---

### Phase 2 Dependencies

- Phase 1 schema defined
- Open question from PRD §10 must be answered before designing the profile update format: **"How should repeated mistakes be categorized?"**

### Phase 2 Complexity

**Medium.** Each individual capability is straightforward. The complexity is in consistency: all three must write to the profile in a compatible format so the Sprint Planner can read a unified view in Phase 3.

### Why before Phase 3

Sprint Planning reads the Learning Profile. With only Phase 1 seed data, it can produce a Sprint — but a generic one. Running Phase 2 for even a few real interactions gives the planner actual practice history and real mistake patterns to reason from. Phase 2 also has standalone daily value independent of Sprint Planning.

---

## Phase 3 — Sprint Planning

### Goal

Build the Sprint Planner as a read-only consumer of the accumulated Learning Profile. Produce Sprint-001 manually as a quality baseline.

### Deliverables

| File | Purpose |
| ---- | ------- |
| `08_ai/templates/sprint_plan.md` | Sprint template: Goal, Practice Priorities (from profile weaknesses), Daily Plan, Teacher Recommendations (from personas), Acceptance Criteria, Sprint Review Checklist |
| `CLAUDE.md` update | Sprint Planner instructions: read full profile + all teacher personas → reason about highest-impact focus → output Sprint. Must not recommend anything unsupported by the profile. |
| `09_coach/sprints/sprint-001.md` | Sprint-001, generated manually to validate the planner quality |

### Dependencies

- Phase 1 done
- Phase 2 has run for at least a few real interactions
- Open question from PRD §10 to resolve: **"How should conflicting teacher opinions be resolved?"**

### Complexity

**Medium.** Template is low complexity. The CLAUDE.md instructions are the hard part: the planner must derive priorities visibly from the profile, not from generic IELTS advice.

### Why before Phase 4

Can't review a Sprint that doesn't exist.

---

## Phase 4 — Sprint Review & Continuous Learning

### Goal

Close the loop. Review Sprint results, capture evidence of progress or continued weakness, and write that evidence back into the Learning Profile to improve the next Sprint.

### Deliverables

| File | Purpose |
| ---- | ------- |
| `08_ai/templates/sprint_review.md` | End-of-Sprint template: goals met?, repeated mistakes still present, profile updates needed |
| `09_coach/sprints/sprint-001-review.md` | Sprint-001 review, completed manually |
| `CLAUDE.md` update | Sprint Review instructions; always ends with proposed profile update |
| `09_coach/connie_profile.md` update | First Sprint-evidence-based profile update |

### Dependencies

- Sprint-001 running for at least one week (Phase 3)
- Open questions from PRD §10 to resolve: **"What information should every Sprint Review capture?"** and **"What evidence determines Sprint success?"**

### Complexity

**Medium.** The meaningful complexity is in how Sprint Review evidence updates the profile in a way that the next Sprint call actually produces a different, better recommendation.

### Why before Phase 5

Phase 5 automates the full loop. The complete manual cycle — Practice Review → profile update → Sprint → Sprint Review → profile update → next Sprint — must be validated before encoding any part of it.

---

## Phase 5 — Automation

### Goal

Replace manual triggers with Claude Code commands. Every daily capability becomes a single command. The manual path stays available.

| Command | Behaviour |
| ------- | --------- |
| `批改` (extended) | Practice Review → feedback + proposed profile update, auto-saved to correct folder |
| `更新筆記` (extended) | Lesson transcript → notes update + proposed profile update |
| `更新學習紀錄` | Append approved evidence to profile |
| `建立 Sprint` | Read full profile + all teacher personas → generate Sprint → save to `09_coach/sprints/` |
| `Sprint 回顧` | Sprint Review → save review + propose profile update |

Sprint-002 is the first automatically generated Sprint. It is manually validated against Sprint-001 quality before treating automation as the default path.

### Dependencies

- One complete manual loop validated (Phases 2–4)
- All templates from Phases 2–4 finalized
- Open question resolved: **"What evidence determines Sprint success?"**

### Complexity

**Medium–High.** No application code. The challenge is prompt design: automated commands must match the manual baseline. Expect 2–3 CLAUDE.md iterations per command.

### Why last

PRD principle: validate manually before automating. Every phase above produces a manual artifact that Phase 5 then automates. Skipping to automation before the manual loop is proven only makes errors harder to diagnose.

---

## Summary

| Phase | Focus | Daily value without later phases? | Complexity |
| ----- | ----- | --------------------------------- | ---------- |
| 1 | Connie Profile + Teacher Personas library | Partial (profile exists but nothing writes to it) | Low–Medium |
| 2 | Practice Review · Knowledge Extraction · Profile Updates | **Yes — usable daily on its own** | Medium |
| 3 | Sprint Planner + Sprint-001 | Yes, but richer with Phase 2 data | Medium |
| 4 | Sprint Review + Continuous Learning | Completes the loop | Medium |
| 5 | Automation of all capabilities | Reduces friction; not functionally new | Medium–High |

---

## Immediate Blocker

Before Phase 1 can start:

> **What are Connie's current IELTS scores (actual or self-assessed per skill: Listening / Reading / Writing / Speaking)?**

This is the anchor point of the Learning Profile. All weakness analysis, Sprint priorities, and teacher recommendations derive from it.
