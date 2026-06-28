# Reading Performance Database

> Machine-readable. Source of truth for Reading skill tracking.
> Claude must update this file after every Reading test session.
> Do not convert a single mistake into a permanent weakness — wait for pattern confirmation.

---

## Purpose

Claude should use this database to:
- track Reading performance by Cambridge test
- identify weak question types
- identify recurring reasoning errors
- update `09_coach/connie_profile.md`
- generate targeted Reading practice plans

---

## Overall Summary

| Field | Value |
|---|---|
| Current estimate | Band 7.0–8.0 |
| Test data range | Band 8.0 (C20 T1) |
| Target | Band 7.0 |
| Gap | ✅ At/above target |
| Tests logged | 1 |
| Last updated | 2026-06-28 |

**Overall assessment:** Reading is currently one of Connie's stronger skills. Main bottleneck is not vocabulary or basic comprehension — it is evidence verification, main idea extraction, and precise answer extraction.

---

## Historical Scores

| Book | Test | Band | S1 (score/total) | S2 (score/total) | S3 (score/total) | Total | Accuracy |
|---|---|---|---|---|---|---|---|
| C20 | T1 | 8.0 | 13/14 (92.9%) | 12/13 (92.3%) | 9/13 (69.2%) | 34/40 | 85.0% |

---

## C20 Test 1 — Section 3 Breakdown

| Questions | Question Type | Score | Accuracy | Notes |
|---|---|---|---|---|
| 28–32 | Matching Information / Paragraph Matching | 4/5 | 80% | One error: related paragraph found but evidence not fully verified |
| 33–36 | Multiple Choice | 3/4 | 75% | One error: supporting detail confused with correct answer |
| 37–39 | Summary Completion | 2/3 | 66.7% | One error: wrong word extracted from correct sentence |
| 40 | Title / Main Idea | 0/1 | 0% | Error: chose memorable story detail instead of article's central purpose |

---

## Observed Error Cases

### Q28 — Matching Information

| Field | Value |
|---|---|
| Correct answer | B |
| Connie's answer | E |
| Error categories | incomplete evidence verification · related paragraph trap · premature conclusion |

**Diagnosis:** Found a topically related paragraph but did not fully verify whether it matched the exact statement conditions.

---

### Q35 — Multiple Choice

| Field | Value |
|---|---|
| Correct answer | B |
| Connie's answer | D |
| Error categories | supporting detail trap · evidence verification error |

**Diagnosis:** Selected an option related to the story content, but not specifically supported by the text for that question.

---

### Q39 — Summary Completion

| Field | Value |
|---|---|
| Correct answer | workshop |
| Connie's answer | coming |
| Error categories | wrong word extraction · grammar fit error · noun phrase identification error |

**Diagnosis:** Understood the general sentence but extracted the wrong word. Answer required the noun phrase connected to "Seaton workshop."

---

### Q40 — Title / Main Idea

| Field | Value |
|---|---|
| Correct answer | C |
| Connie's answer | A |
| Error categories | main idea extraction error · story detail trap · article purpose missed |

**Diagnosis:** Focused on an interesting event in the passage. Missed the article's broader purpose: the benefits for children of working with archaeologists.

---

## Weakness Profile

### 1. Main Idea Extraction

| Field | Value |
|---|---|
| Priority | High |
| Confidence | Medium–High |
| Affected types | Title questions · passage summary |

Pattern: Focuses on memorable details rather than the author's overall message.

Symptoms:
- chooses an interesting event as the title
- confuses story content with article purpose
- misses repeated themes across paragraphs
- focuses on "what happened" instead of "what the author is trying to show"

**Training rule:** After reading a passage, ask: "What is the author's main purpose?" Do not choose a title based only on the most memorable example.

---

### 2. Evidence Verification

| Field | Value |
|---|---|
| Priority | High |
| Confidence | High |
| Affected types | Matching Information · Matching Features · TFNG · Multiple Choice · Title/Main Idea |

Pattern: Finds the relevant paragraph quickly, but sometimes selects before verifying all conditions.

Wrong process: keyword found → related paragraph found → answer selected

Target process: keyword found → paragraph found → **all conditions verified** → alternatives compared → answer selected

---

### 3. Precise Answer Extraction

| Field | Value |
|---|---|
| Priority | Medium |
| Confidence | Medium |
| Affected types | Summary Completion · Note Completion · Short Answer |

Pattern: Understands general meaning but extracts the wrong word.

Common risks: choosing a nearby word · wrong part of speech · ignoring grammar fit · missing exact noun phrase

**Training rule:** For completion tasks, identify the required part of speech before searching.

---

## Cross-Skill Pattern — Critical

### Premature Conclusion Before Verification

| Field | Value |
|---|---|
| Priority | Critical |
| Confidence | High |
| Skills affected | Reading · Writing · Listening |

This pattern appears across all three skills:

| Skill | Manifestation |
|---|---|
| Reading | Chooses title based on story detail instead of author's purpose; selects answer after finding one matching keyword without checking all conditions |
| Writing | Answers Agree/Disagree as if it were Positive/Negative; states position without fully checking what the question is actually asking |
| Listening | Chooses answer after hearing a keyword before processing the full condition or post-correction |

**Global coaching rule:** Before giving Connie more vocabulary or speed practice, check whether the real problem is task identification, evidence verification, full condition matching, main idea extraction, or answer precision.

**Evidence:** C20 T1 Q28, Q35, Q40 (Reading) · `01_lessons/writing/writing-lesson_2026-06-19.md` (Writing) · `09_coach/performance/listening_db.md` (Listening distractor pattern)

---

## Current Reading Priorities

| Rank | Focus | Reason |
|---|---|---|
| 1 | Evidence Verification | High confidence; affects multiple question types |
| 2 | Main Idea / Title | Highest-value single question type; 0% in C20 T1 |
| 3 | Matching Information / Features | Related to evidence verification pattern |
| 4 | Precise Answer Extraction (Completion) | 66.7% in C20 T1 summary completion |
| 5 | TFNG / YNNG strict comparison | Adjacent to evidence verification weakness |

---

## Do Not Prioritize by Default

- general vocabulary expansion
- more skimming practice
- generic reading speed drills

**Reason:** Current evidence shows reading level is already strong. Limiting factor is not comprehension or vocabulary.

---

## Question Type Accuracy (Cumulative)

*Based on C20 T1 only — more data needed for reliable conclusions.*

| Question Type | Sessions | Avg Accuracy | Confidence | Priority |
|---|---|---|---|---|
| Form/Note Completion | — | — | Low | — |
| Matching Information | 1 | 80% | Low | Monitor |
| Multiple Choice | 1 | 75% | Low | Monitor |
| Summary Completion | 1 | 66.7% | Low | Monitor |
| Title / Main Idea | 1 | 0% | Low | High — needs more data |
| Matching Features | 0 | — | Low | — |
| TFNG / YNNG | 0 | — | Low | — |

*Promotion rules: below 75% across 3+ tests → High Priority. Above 85% across 5 consecutive tests → Maintenance only.*

---

## Adding New Test Sessions

```markdown
| YYYY-MM-DD | C[book] T[n] | band | S1 (score/total) | S2 (score/total) | S3 (score/total) | total/40 | accuracy% |
```

For every wrong answer, add an Observed Error Case entry with: question number · type · correct answer · Connie's answer · error categories · diagnosis.

After 3+ sessions on the same question type, update the Cumulative Accuracy table and recalculate priority.
