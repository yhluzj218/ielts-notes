# Listening Performance Database

## Purpose

This file stores Connie's historical IELTS Listening performance.

Unlike lesson notes, this file is intended to be machine-readable.

Claude should use this database to:

- identify recurring weaknesses
- calculate question type accuracy
- identify improvement trends
- update `09_coach/connie_profile.md` automatically
- recommend future practice priorities

---

## Overall Statistics

**Books completed:** Cambridge 16, Cambridge 17, Cambridge 20 (partial)

**Current estimated level:** Band 6.0–6.5 *(aligned with connie_profile.md)*

### Section Averages (across all completed tests)

| Section | Average Score | Strength Rating | Status |
|---------|:------------:|-----------------|--------|
| S1 | 6.5 / 10 | ★★★★☆ | Stable |
| S2 | 7.5 / 10 | ★★★★★ | Strongest |
| S3 | 6.9 / 10 | ★★★★☆ | Medium |
| S4 | 5.1 / 10 | ★★☆☆☆ | **Weakest — High Priority** |

### Current Pattern

**Strengths:** Section 2 · basic conversations · form completion · stable everyday listening

**Weaknesses:** Section 4 · long monologues · lecture note completion · long-term concentration · fast paraphrase processing

**Confidence in assessment:** Medium — question-type breakdown still incomplete; current data based on section scores only.

---

## Historical Scores

| Book | Test | Band  | S1  | S2  | S3  | S4  |
|------|------|-------|-----|-----|-----|-----|
| C16  | T1   | 6.5   | 8   | 6   | 8   | 6   |
| C16  | T2   | 7.0   | 9   | 7   | 8   | 8   |
| C16  | T3   | 6.5   | 9   | 7   | 7   | 5   |
| C16  | T4   | Incomplete | 6 | — | — | — |
| C17  | T1   | 5.0   | 0   | 7   | 6   | 3   |
| C17  | T2   | 6.5   | 7   | 9   | 6   | 5   |
| C17  | T3   | 5.5   | 5   | 8   | 4   | 4   |
| C17  | T4   | 7.0   | 7   | 10  | 7   | 6   |
| C20  | T1   | 6.0   | 7   | 6   | 9   | 4   |

---

## Sprint S4 Standalone Drill Log

*Separate from full Cambridge test records. Pattern tracking within sprints.*

| Date | Source | S4 Score | Error Types |
|---|---|---|---|
| 2026-06-30 | Sprint-001 Tue D1 (food trends lecture) | 4/10 | word/phrase ×4 · qualifier trap ×1 · concentration drop ×1 |

**2026-06-30 detail:**
- Q31 singular/plural · Q32 misheard (virgin → vegan) · Q33 concentration drop · Q34 singular/plural · Q36 word count exceeded (wrote "coffee-chain") · Q39 qualifier trap (locked on "financially" before "price soared")
- Confirmed: singular/plural weakness active in Note Completion
- Confirmed: Premature Conclusion Before Verification active in S4 (Q39 → links to `connie_profile.md` §4.0)

---

## Section Profiles

### Section 1 (Average: 6.5 / 10)

Typical question types: Form Completion · Note Completion

Typical errors: spelling · singular/plural · numbers · names

Assessment: Strength — stable but not perfect.

---

### Section 2 (Average: 7.5 / 10)

Typical question types: Matching · Multiple Choice · Map · Plan

Assessment: Strongest section. Good understanding of conversations.

Note: Section 2 contains multiple question types — needs further breakdown before conclusions about specific types can be drawn.

---

### Section 3 (Average: 6.9 / 10)

Typical question types: Discussion · Multiple Choice · Matching

Weakness: long paraphrases · distracted by similar options

---

### Section 4 (Average: 5.1 / 10) — ⚠️ Highest Priority

Typical question types: Lecture · Note Completion · Summary Completion

Problems:
- concentration drops in long monologues
- paraphrase speed too slow
- spelling errors
- singular/plural confusion
- missing key information while writing answers

---

## Question Type Database

**Status: Preliminary** — to be verified against Cambridge official tests as more data is collected.

| Question Type     | Estimated Strength | Confidence |
|-------------------|--------------------|------------|
| Form Completion   | High               | High       |
| Note Completion   | Medium             | Medium     |
| Multiple Choice   | Medium             | Medium     |
| Matching          | Unknown            | Low        |
| Map               | Unknown            | Low        |
| Plan              | Unknown            | Low        |
| Table Completion  | Unknown            | Low        |
| Diagram           | Unknown            | Low        |

---

## Learning Pattern

Current listening problems are NOT caused by basic comprehension.

Most mistakes happen during:
- fast paraphrase recognition
- answer verification under time pressure
- distractor handling
- maintaining concentration across long monologues
- processing information while writing answers simultaneously

---

## Current Priorities

| Rank | Focus | Reason |
|------|-------|--------|
| 1 | Section 4 | Lowest average (5.1) across all completed tests |
| 2 | Lecture Note Completion | Spelling · grammar fit · singular/plural · paraphrase |
| 3 | Multiple Choice | Distractors · transition words · answer verification |
| 4 | Matching | Option labelling · paraphrase grouping · choosing quickly |

---

## Automatic Update Rules (for Claude)

Whenever a new test is added to Historical Scores:

1. Recalculate section averages.
2. Recalculate question type averages (when data is available).
3. Detect improving trends (3+ consecutive tests improving in a section).
4. Detect recurring weaknesses (section average below 6.0 across 3+ tests).
5. Update `09_coach/connie_profile.md` § 7 (Listening Profile) automatically.
6. If any question type remains below 70% accuracy across 5+ tests → mark as High Priority.
7. If any question type improves above 85% for 5 consecutive tests → remove from High Priority.
8. Never recommend generic listening practice before checking this database.
9. Always prioritize practice according to historical evidence, not just recent performance.

---

## Adding New Test Results

When a new Cambridge test is completed, append using this format:

```markdown
### [Book] Test [N] — [Date]

| Field | Value |
|---|---|
| Band | X.X |
| S1 | X / 10 |
| S2 | X / 10 |
| S3 | X / 10 |
| S4 | X / 10 |

**Question type breakdown:**

| Section | Question Type | Score |
|---------|---------------|-------|
| S1 | Form Completion | X / 10 |
| S2 | Matching | X / 5 |
| S2 | Map | X / 5 |
| S3 | Multiple Choice | X / 10 |
| S4 | Lecture Note Completion | X / 10 |

**Error categories this test:**
- [ ] distractor
- [ ] paraphrase
- [ ] spelling
- [ ] grammar fit
- [ ] singular/plural
- [ ] prediction failure
- [ ] concentration drop (S4)

**Review file:** `04_listening/reviews/[book]-[test].md`
```
