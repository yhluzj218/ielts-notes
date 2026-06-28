# Implementation Plan — AI IELTS Coach MVP

> This implementation plan follows the PRD. Product decisions belong to the PRD. This document only describes the implementation sequence.

---

# MVP Philosophy

The AI IELTS Coach is **not a Sprint generator**.

It is a **personal IELTS learning system** that continuously helps Connie improve through:

* Practice Review
* Teacher Knowledge
* Learning Profile
* Sprint Planning

Sprint Planning is the decision engine of the system, not the only capability.

---

# Core Learning Loop

```text
IELTS Practice
        │
        ▼
Practice Review
        │
        ▼
Learning Profile
        ▲
        │
Teacher Knowledge
        │
        ▼
Sprint Planner
        │
        ▼
Next Sprint
```

Every interaction should improve the Learning Profile.

Every Sprint should become better than the previous one.

---

# Phase 1 — Build the Learning Foundation

## Goal

Build the knowledge structures that every future capability depends on.

Without these foundations, all recommendations become generic.

## Deliverables

| File                                | Purpose                                  |
| ----------------------------------- | ---------------------------------------- |
| `09_coach/connie_profile.md`        | Connie's evolving learning profile       |
| `08_ai/teachers/matt.md`            | Matt's methodology                       |
| `08_ai/teachers/joe.md`             | Joe's methodology                        |
| `08_ai/templates/profile_update.md` | Standard format for updating the profile |

## Why First

Everything depends on understanding Connie.

No profile means no personalization.

---

# Phase 2 — Build Learning Capabilities

## Goal

Allow the AI coach to understand different learning inputs.

## Deliverables

### Practice Review

Support:

* Writing
* Speaking
* Listening
* Reading

Each review should:

* identify repeated mistakes
* update Learning Profile
* recommend whether Sprint adjustment is needed

---

### Teacher Knowledge Builder

Input:

Lesson transcript

Output:

* Teacher principles
* Teaching philosophy
* Common recommendations
* New coaching patterns

Teacher knowledge should evolve over time instead of remaining static.

---

### Knowledge Updater

Every interaction should update:

* Connie Profile
* Teacher Knowledge
* Learning History

without overwriting previous knowledge.

## Why Second

The coach should first learn before it starts making planning decisions.

---

# Phase 3 — Sprint Planning

## Goal

Generate personalized Sprint plans using everything accumulated so far.

## Deliverables

| File                             | Purpose                    |
| -------------------------------- | -------------------------- |
| `08_ai/templates/sprint_plan.md` | Sprint template            |
| `09_coach/sprints/sprint-001.md` | First Sprint               |
| `CLAUDE.md` update               | Sprint generation workflow |

Sprint should include:

* Goal
* Daily Practice
* Weekly Priorities
* Teacher Recommendations
* Acceptance Criteria
* Review Checklist

## Why Third

Sprint planning is only useful when sufficient learning evidence already exists.

---

# Phase 4 — Sprint Review & Continuous Learning

## Goal

Validate whether the Sprint actually improved Connie's IELTS ability.

## Deliverables

Support collecting evidence from:

* Writing
* Speaking
* Listening
* Reading
* Mock Tests
* Teacher Feedback

Then:

* evaluate Sprint effectiveness
* update Learning Profile
* improve future Sprint recommendations

## Why Fourth

Without evidence, the system cannot learn.

---

# Phase 5 — Automation

## Goal

Automate the complete learning workflow using Claude Code.

## Deliverables

Commands such as:

* 建立 Sprint
* 批改作文
* 批改口說
* 分析 Listening
* 更新 Connie Profile
* 更新 Teacher Persona
* 整理老師逐字稿

Every command should ultimately improve the Learning Profile.

Automation should never bypass the manual learning workflow validated in previous phases.

---

# Summary

| Phase | Focus                 |
| ----- | --------------------- |
| 1     | Learning Foundation   |
| 2     | Learning Capabilities |
| 3     | Sprint Planning       |
| 4     | Continuous Learning   |
| 5     | Automation            |

---

# MVP Success

At the end of MVP, Connie should be able to:

✅ Paste a writing draft and receive personalized feedback.

✅ Paste a speaking transcript and receive personalized feedback.

✅ Paste a lesson transcript and automatically update Teacher Knowledge.

✅ Paste Listening or Reading practice and identify repeated weaknesses.

✅ Generate a personalized Sprint based on all accumulated knowledge.

✅ Continuously improve the Learning Profile after every learning activity.

---

# Current Blocker

Before implementation begins, the following must be defined:

* Connie Profile structure
* Teacher Persona structure
* Sprint template
* Learning Profile update rules

These schemas will become the foundation of every future feature.
