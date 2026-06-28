# Coach Conflicts

> This file logs areas where coaches disagree.
> Per ADR-007: Do NOT resolve conflicts silently. List both positions. Ask Connie to decide.
> See `DECISIONS.md` for ADR-007.
> Last updated: 2026-06-28

---

## Format

Each conflict entry:
- States both positions in one sentence each
- Notes confidence level (how certain we are this is a real conflict vs a gap)
- Notes what decision is needed from Connie

---

## Active Conflicts

### Conflict: Vocabulary as a priority

| Field | Value |
|---|---|
| Simon | "Vocabulary is the key to a higher IELTS score" — general advice for all students; vocabulary > grammar for English improvement |
| Matt | "My instinct is not that you have a lack of vocabulary" — Connie-specific; vocabulary is a confirmed strength, not the bottleneck |
| Joe | "Connie thinks she lacks vocabulary, but she doesn't" — Connie-specific; same conclusion as Matt |
| Confidence | High — all three positions are explicitly stated |
| Discovered | 2026-06-28, `knowledge/coaches/simon/originals/3-keys-preparation_2026-06-28.md` |
| Decision needed | Simon's advice is for general IELTS students. Matt and Joe have directly assessed Connie and agreed she is an exception. **Default rule: apply Matt + Joe's Connie-specific assessment. Do not recommend vocabulary work unless Connie explicitly requests it.** |
| Resolution | ✅ Resolved by personal teacher assessment — Matt + Joe override Simon for this learner |

---

## Pending Clarifications (Gaps, Not Conflicts)

These are areas where one coach has addressed a topic but others have not — not confirmed disagreements.

| Area | Known Position | Missing Input | Status |
|---|---|---|---|
| Authentic English exposure (BBC, Guardian etc.) | Simon: start when approaching Band 7+ | Matt and Joe: not addressed | ⚠️ Gap — ask Matt if he recommends authentic reading for Writing improvement |
| Shadowing for pronunciation | Matt: yes, but only after intonation lesson | Joe: not addressed; Simon: not addressed | ⚠️ Gap — Joe should clarify if shadowing is also recommended from his approach |
| Model essay imitation | None of the coaches have directly recommended or warned against this | — | ⚠️ Gap — ask Matt or Joe before including in a sprint |
| Grammar systematic study | Simon: anti-pattern (use own errors) | Matt: same — but hasn't explicitly said "never do grammar exercises" | ⚠️ Partial — assume consensus unless Matt specifies otherwise |

---

## Resolved Conflicts

*None yet.*

---

## How to Add a Conflict

When a new lesson produces coach guidance that contradicts an existing principle:

```markdown
### Conflict: [Short description]

| Field | Value |
|---|---|
| Coach A | [Name]: [their position in one sentence] |
| Coach B | [Name]: [their position in one sentence] |
| Confidence | High / Medium / Low |
| Discovered | YYYY-MM-DD, lesson reference |
| Decision needed | [What Connie needs to choose between] |
| Resolution | Pending / [Connie's decision + date] |
```
