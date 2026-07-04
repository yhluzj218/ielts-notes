# Coach Conflicts

> This file logs areas where coaches disagree.
> Per ADR-007: Do NOT resolve conflicts silently. List both positions. Ask Connie to decide.
> See `DECISIONS.md` for ADR-007.
> Last updated: 2026-07-02

---

## Format

Each conflict entry:
- States both positions in one sentence each
- Notes confidence level (how certain we are this is a real conflict vs a gap)
- Notes what decision is needed from Connie

---

## Active Conflicts

### Conflict: "Template" writing — is the project's Introduction/Conclusion Template the banned kind?

| Field | Value |
|---|---|
| Joe (writing course) | Any memorised, fill-in-the-gap template caps the essay at Band 2 — examiners recognise repeated templates and see grammar break down between memorised chunk and own content. |
| Project (`10_knowledge_base/writing/writing_patterns.md` §5, §7) | Uses fixed sentence frames explicitly named "Introduction Templates" / "Conclusion Templates", e.g. `[Paraphrase of topic]. [This essay will argue that + your position + one-line reason.]` — position/content is meant to be filled fresh each time; only the connector phrase is fixed. |
| Confidence | Medium-High — see new evidence below, which points toward "not a real conflict" |
| Discovered | 2026-07-02, `10_knowledge_base/coaches/joe/originals/writing-mistake-02-using-a-template_2026-07-02.md` |
| New evidence (2026-07-02, live group writing lesson, clean high-confidence transcript) | Joe personally dictated this exact intro sentence in class: `"This essay argues that these changes have been transformative because consumers can buy things from other countries and sell things online."` — structurally identical to the project's own Introduction Template pattern. Joe teaching this himself right after warning against templates strongly suggests his warning targets fully-memorised generic social-media templates, not connector-only skeleton frames. Source: `01_lessons/writing/writing-lesson_2026-07-02.md`. |
| Decision needed | Confirm: is this now resolved (project's templates ≠ the banned kind), or do you still want to ask Matt / adjust naming to be safe? |
| Resolution | Pending your confirmation — recommend closing as "not a conflict" given the lesson evidence |

---

### Conflict: Vocabulary as a priority

| Field | Value |
|---|---|
| Simon | "Vocabulary is the key to a higher IELTS score" — general advice for all students; vocabulary > grammar for English improvement |
| Matt | "My instinct is not that you have a lack of vocabulary" — Connie-specific; vocabulary is a confirmed strength, not the bottleneck |
| Joe | "Connie thinks she lacks vocabulary, but she doesn't" — Connie-specific; same conclusion as Matt |
| Confidence | High — all three positions are explicitly stated |
| Discovered | 2026-06-28, `10_knowledge_base/coaches/simon/originals/3-keys-preparation_2026-06-28.md` |
| Decision needed | Simon's advice is for general IELTS students. Matt and Joe have directly assessed Connie and agreed she is an exception. **Default rule: apply Matt + Joe's Connie-specific assessment. Do not recommend vocabulary work unless Connie explicitly requests it.** |
| Resolution | ✅ Resolved by personal teacher assessment — Matt + Joe override Simon for this learner |
| 2026-07-02 update | Joe's own video course now includes a generic "vocabulary can improve your score" section (`10_knowledge_base/coaches/joe/originals/writing-vocabulary-intro_2026-07-02.md`). Same resolution applies: this is generic course content for all students, not a new Connie-specific assessment from Joe — it does not reopen this conflict. |

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
