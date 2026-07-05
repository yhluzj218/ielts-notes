# Sprint-001

> Duration: 2026-07-06 (Mon) — 2026-07-19 (Sun)
> Assessment point: Matt writing lesson confirmed 2026-07-15, 21:15 (Wed, Week 2)
> Last updated: 2026-07-04 (Week 1 rebuilt around confirmed italki calendar — see § 5 Week 1 note)
> Template version: v2.0

> **Reset note (2026-07-04):** The original 2026-06-29 — 2026-07-05 week is discarded.
> Tracking got confusing (tasks were done but not logged/reviewed), so rather than
> reconstruct it, the sprint restarts clean from Monday 2026-07-06. Nothing from the
> discarded week was entered into any DB, so there is nothing to roll back — this is
> a clean restart, not a correction.

---

## 1. Sprint Goal

Fix the Writing method before Matt's lesson on ~July 15.

Three specific targets:
1. Identify the question type correctly before planning every essay
2. Build complete body paragraphs — the chain must reach result/consequence level
3. Establish skeleton-first as a non-negotiable habit

Secondary: Apply S4 verification method and reduce distractor/qualifier trap rate.

This sprint targets **method**, not language. Do not change the method because it feels difficult — score fluctuation is normal while a new method is being internalised (Simon).

---

## 2. Weekly Main Objective

| Week | Dates | Objective | Difficulty |
|---|---|---|---|
| Week 1 | Mon 7/6 — Sun 7/12 | Method acquisition — **overridden to D2/D3 this week only** by real Joe offline-lesson deadlines (2 new full essays + 1 finished essay for a live lesson); see § 5 Week 1 note | D1 → D2/D3 (forced by real deadlines) |
| Week 2 | Mon 7/13 — Sun 7/19 | Method under pressure — apply the tools in timed conditions | D2 → D3 |

**Difficulty levels:**
- D1: Untimed, low pressure — drills and skeleton writing
- D2: Partial timing — timed body paragraphs, section-only listening
- D3: Full exam-like — timed essay (60 min), full Cambridge test

---

## 3. Fixed Weekly Rhythm

This rhythm repeats every week. Commute slots and evening slots are separate.

| Day | Commute (1.5h) | Evening (~90 min) |
|---|---|---|
| **Mon** | Podcast (45 min) + Speaking Part 2 out loud (45 min) | Writing: question type + skeleton |
| **Tue** | Podcast (45 min) + Speaking Part 3 out loud (45 min) | Listening: Cambridge S4 + transcript analysis |
| **Wed** | Podcast (45 min) + Shadowing (45 min) | Writing: body paragraph or full essay |
| **Thu** | Podcast (45 min) + Joe lesson warm-up Part 2 (45 min) | **Joe Speaking Lesson** + correction notes |
| **Fri** | Podcast (45 min) + light review (45 min) | Matt Writing Lesson OR essay prep/rewrite |
| **Sat** | Optional podcast | Buffer / catch-up / sprint review (see § 9) |
| **Sun** | — | **Full Mock** + error analysis (see § 7) |

**Commute constraints:**
- No writing. No question sheets. No transcript analysis.
- Podcast = active listening: follow the argument, catch the main point, notice unfamiliar chunks
- Part 2 speaking = out loud at full speed, timed for 2 minutes
- Part 3 speaking = give a societal-level answer, not just personal experience

---

## 4. Daily Commute Podcast Plan

### Podcast Template File

The automatic nightly Episode Package workflow is disabled. Phase 1 can generate
only a source-grounded NotebookLM brief after Connie supplies an IELTS question,
model essay, article, notes, or viewpoints. Research-Assisted Mode may supplement
that material with logged, credible external sources. Briefs are stored in
`07_podcast/source_briefs/`. Stage 2 can generate ElevenLabs/TTS controlled output
practice only after Connie supplies a Core Pattern, Model Sentence, and three to
five Vocabulary / Expressions and passes the context gate.

### Weekly Podcast Focus

| Day | Podcast Focus | Commute Speaking |
|---|---|---|
| Mon | Part 2 storytelling + Sunday mock review | Part 2: personal topics (hobby / place / event) |
| Tue | Part 3 opinion language + Listening skill tip | Part 3: society-level opinions |
| Wed | Shadowing + Writing sentence chunks | Shadowing: repeat-after-audio |
| Thu | Joe lesson warm-up | Part 2: complete one topic with full 2-min run |
| Fri | Light review + Matt writing prep | Speak freely — no pressure |
| Sat | Optional weekly review | Optional Part 2 for enjoyment |
| Sun | Optional: mock mindset prompts | — |

### Night-Before Prep Steps

There is no automatic night-before generation.

If Connie has selected source material:

1. Provide the IELTS question, model essay, article, notes, or viewpoints.
2. Trigger `生成 Podcast` or `根據這些資料產生 NotebookLM source brief`.
3. Review the grounded brief and NotebookLM Generation Prompt.
4. After NotebookLM listening, provide `# Output Drill Input` and trigger
   `產生 Output Drill Script` if controlled speaking practice is wanted.
5. For a final memory song, provide `# Chant Input` with the Target Sentence Pattern
   and trigger `產生 Chant`.

---

## 5. Evening Study Plan

### Week 1 — Method Acquisition, accelerated by real Joe deadlines (Mon 7/6 — Sun 7/12)

> ⚠️ **This week's plan is overridden by real italki bookings, confirmed 2026-07-04:**
> Joe now has three touchpoints this week — Tue 7/7 (offline, essay due the **night
> before**, i.e. Mon 7/6 night), Thu 7/9 (live video — but you must arrive with the
> **7/2 lesson's unfinished essay completed**), and Sat 7/11 (offline, essay due the
> **night before**, i.e. Fri 7/10 night). 7/7 and 7/11 each need a **new, separate**
> essay — not the same one revised twice. This means Week 1 is no longer pure D1
> (untimed drills) — it's three real full essays with real deadlines. The skeleton
> step is not optional just because it's rushed; keep it. If this Joe cadence
> continues past this week, revisit the Fixed Weekly Rhythm in §3 for Sprint-002 —
> for now this is a one-week override, not a permanent rhythm change.

---

#### Mon 7/6 — Full Essay #1, due tonight for Tue 7/7 offline (100 min)

**Why:** Joe's offline review needs your essay by tonight. This replaces the original
untimed skeleton-only drill — same method, real stakes.

**Timer structure:**
- 5 min: pick a Task 2 prompt (Cambridge past paper) → question type + position
- 10 min: skeleton (4-part — non-negotiable even under deadline pressure)
- 60 min: full essay — write continuously, no stopping to edit
- 15 min: self-review (question type correct? position clear in intro? both body
  paragraphs reach [result] level? conclusion restates, no new points?)
- 10 min: error scan — G001, G003, G010, G011

Save as `02_writing/task2/drafts/[topic]_2026-07-06.md` (use `建草稿` if you want me
to format it). **Submit to Joe tonight — this is the actual deadline, not a buffer.**

---

#### Tue 7/7 — Joe offline review (essay already submitted) + Listening D1 (90 min evening)

No writing task today — Monday night's essay is already in Joe's hands. Evening slot
reverts to the original plan:

**Cambridge S4 + Transcript Analysis**

**Why:** S4 average 5.1/10 — weakest section across all Cambridge tests. The
cross-skill "Premature Conclusion Before Verification" pattern (`connie_profile.md`
§4.0) causes locking in before the full condition is stated.

**Step 1 — Before audio (10 min)**
- Read all S4 questions
- Underline differentiating keywords — words that make the options different from each other, not words all options share
- For Note Completion: predict word type before the audio starts (noun? number? adjective?)

**Step 2 — Listen and answer (35 min)**
- Do not write after the first keyword
- Watch for: qualifier traps · self-corrections ("oh sorry, I meant...") · conditional branches

**Step 3 — Transcript analysis (45 min)**

For every wrong answer:
1. Find the correct answer in the transcript
2. Find the words that eliminate each wrong option
3. Classify the error type:
   - `word/phrase` — paraphrase not recognised
   - `misunderstood` — heard it, processed it wrong
   - `stuck on previous` — missed it while still writing the last answer
   - `qualifier trap` — chose the first word before the full condition
   - `self-correction missed` — missed the "oh sorry" correction
   - `concentration drop` — lost the thread in a long monologue

**Review**
- [ ] Used differentiating keywords (not all keywords)?
- [ ] Avoided locking in before the full condition was heard?
- [ ] Classified every wrong answer with a specific error type?

Report to me: S4 score + error categories. I will update `listening_db.md`.

---

#### Wed 7/8 — Finish the 7/2 lesson's unfinished essay, due tomorrow's live lesson (90 min)

**Why:** Thu 7/9 is a live Joe lesson — you need the 7/2 essay (online shopping /
new technologies, opinion essay) finished, not a fresh drill. This IS body paragraph
development practice — just applied to real homework instead of a generic prompt.

**What's already done (from `01_lessons/writing/writing-lesson_2026-07-02.md`):**
- Type = opinion essay, Opinion = strongly agree, Reason 1 = more choices, Reason 2 = people selling
- Introduction — fully written in class
- Body 1 — only "Main idea / Explain / Example" labels sketched, not written

**What's left tonight:**
1. Finish Body 1: Main idea → Explain → Example → Result (same chain as always)
2. Write Body 2 (Reason 2: people selling)
3. Write Conclusion

Label every sentence with its job `[point] [explain] [support] [result]` as you write.

**Self-check:**
- [ ] Does every sentence add something new?
- [ ] Does the chain reach `[result]` level or beyond?
- [ ] Are any two sentences doing the same job? → Remove the weaker one

**Error scan (15 min):** G001, G003, G010, G011 — plus check whether `get use of` →
`get used to` (flagged 1st occurrence on 7/2) shows up again; if so, tell me, it
becomes a Low confidence DB entry on 2nd occurrence.

Save/update the draft so you can bring it to tomorrow's lesson.

---

#### Thu 7/9 — Joe live video lesson (bring the finished 7/2 essay)

No other practice today. Save energy for the lesson.

**After lesson:** write 1–2 corrections Joe gave. Log in `01_lessons/writing/writing-lesson_2026-07-09.md`.

---

#### Fri 7/10 — Full Essay #2, due tonight for Sat 7/11 offline (100 min)

Same timer structure as Mon 7/6 — a **new** prompt, not a revision of Monday's essay.

**Timer structure:**
- 5 min: pick a different Task 2 prompt → question type + position
- 10 min: skeleton (4-part)
- 60 min: full essay — write continuously
- 15 min: self-review
- 10 min: error scan

Save as `02_writing/task2/drafts/[topic]_2026-07-10.md`. **Submit to Joe tonight.**

This replaces the original "rest day" — there is no rest day this week because of the
two offline deadlines. Sat 7/11 is the lighter day instead (see below).

---

#### Sat 7/11 — Joe offline review (essay already submitted) + light buffer

Essay is already submitted from Friday night. Use today as the actual light day this
week:
- If Tue 7/7's offline feedback has come back, review it (no new writing required)
- Otherwise: true rest, per § 9 buffer rules

---

#### Sun 7/12 — Full Mock #1

See § 7. Note: this is a demanding week (3 essays + a mock) — if Saturday's rest
wasn't enough, it's fine to keep the mock light on self-analysis depth rather than
skip it.

---

### Week 2 — Method Under Pressure (Mon 7/13 — Sun 7/19)

> ⚠️ **Matt lesson lands mid-week this cycle (~7/15, Wed).** The plan below still puts
> the D3 timed essay on Wed 7/15 evening. If Matt's lesson is in the evening, bring
> Monday 7/13's D2 essay instead — the Wed essay won't exist yet. If Matt's lesson is
> daytime, Wed evening's D3 essay proceeds as normal and Fri 7/17 becomes lesson
> follow-up instead of pre-lesson prep. Confirm the actual lesson time once scheduled.

---

#### Mon 7/13 — Writing D2: Discussion Essay — Argue the Weaker Side (90 min)

**Why:** `writing_db.md` recurring weakness: "Body 1 (weaker side) too superficial." Matt: argue the opposing view as if you believe it — a dismissive paragraph signals inability to engage with opposing ideas.

**Exercise:**
1. Find a Discuss Both Views prompt
2. Identify the view you personally disagree with
3. Write ONLY the body paragraph for that view
4. Argue it fully: reason + example + consequence
5. Read it aloud: does it sound like you believe it, or like you are dismissing it?

**Check:**
- [ ] Reason, example, and consequence all present?
- [ ] Does it avoid "some people think X, however this is wrong"?
- [ ] Does it feel as developed as your own-view paragraph would be?

**Error scan (15 min)**

---

#### Tue 7/14 — Listening D2: Cambridge S4 #2 + Pattern Comparison (90 min)

Same method as Tue 7/7.

**After transcript analysis, compare with last Tuesday:**
- Same error type appearing again? → That is the confirmed priority pattern
- Different error types? → Note which question range (31–34 / 35–37 / 38–40) was harder
- Was there a self-correction you missed again? → That is the primary trap to practise

Report to me: score + error categories. I will update `listening_db.md` and flag any confirmed pattern for Sprint-002.

---

#### Wed 7/15 — Writing D3: First Full Timed Essay (90 min) · Matt lesson ~this day

**Why:** All Week 1 skills tested together under exam conditions. Matt lesson is ~7/15 — see the ⚠️ note above the Week 2 header for how these two interact.

**Timer structure:**
- 5 min: question type + position + structure selection
- 5 min: skeleton (4-part)
- 50 min: full essay — write continuously, no stopping to edit
- 10 min: self-review only (mark questions for Matt, do not rewrite)

Save draft: `02_writing/task2/drafts/[topic]_2026-07-15.md`

**Self-review checklist (mark, do not fix):**
- [ ] Question type correctly identified?
- [ ] Position stated in intro?
- [ ] Body 1 chain reached result/consequence level?
- [ ] Body 2 chain reached result/consequence level?
- [ ] Conclusion restates position?

**Error scan (15 min):** Full error scan. Any error appearing for the second time this sprint → tell me for DB entry.

---

#### Thu 7/16 — Joe Speaking Lesson

No other practice today.

**After lesson:** note 1–2 corrections. Log in `01_lessons/speaking/speaking-lesson_2026-07-16.md`.

---

#### Fri 7/17 — Matt Lesson Prep (90 min)

Use this session to prepare (or, if Matt's lesson already happened on Wed, to follow up — see ⚠️ note above).

Review the Wed 7/15 essay (or Mon 7/13's, if that's what you brought):
1. What question type was this, and are you certain you identified it correctly?
2. Which body paragraph had a more complete chain? Why?
3. Which sentences were doing the same job (duplication)?
4. Did you write the skeleton before starting? Did you follow it?

Prepare 2–3 specific questions for Matt. Examples:
- "Is my question type identification correct for this prompt?"
- "My weakest paragraph was [X]. What is missing from the chain?"
- "I am still unsure when to use Discuss Both Views vs Agree/Disagree — can we review these two prompts?"

---

#### Sat 7/18 — Sprint Retrospective

See § 10.

---

#### Sun 7/19 — Full Mock #2

See § 7.

---

## 6. Lesson Preparation Plan

> ⚠️ **Week 1 exception (confirmed 2026-07-04):** Joe is teaching writing, not
> speaking, this week — Tue 7/7 (offline) and Sat 7/11 (offline) are both writing
> essay submissions, not speaking warm-ups. The "Before Every Joe Lesson (Thursday)"
> table below is the **normal/default** pattern for weeks where Joe teaches speaking
> on Thursdays — it does not apply to Tue 7/7 or Sat 7/11 this week. Prep for those
> two is simply: finish and submit the full essay the night before (see § 5 Week 1,
> Mon 7/6 and Fri 7/10).

### Before Every Joe Lesson (Thursday) — default pattern (speaking weeks)

| When | What |
|---|---|
| Wednesday commute | Speaking Part 2 × 3 topics out loud (45 min) |
| Thursday commute | Full run-through of one Part 2 topic before lesson |
| Thursday evening | Focus entirely on the lesson — no other practice |

**This week (7/9) is a writing lesson, not speaking** — see § 5 Week 1, Thu 7/9:
bring the finished 7/2 essay instead of doing Part 2 warm-up.

### Before Every Matt Lesson (Friday, sometimes Tuesday/Wednesday)

| What to bring | Why |
|---|---|
| Latest timed essay | Real first attempt — do not rewrite before showing |
| 2–3 specific questions written in advance | Matt can address the exact bottleneck |
| No vocabulary lists or extra notes | Matt's focus: task response and development, not vocab |

Tell Matt at the start: "I practised [X] this week. I was uncertain about [Y]. Can we look at [Z]?"

**This sprint: bring `02_writing/task2/drafts/[topic]_2026-07-15.md` to the ~7/15 lesson,
or Monday 7/13's essay if the lesson happens before Wed evening — see ⚠️ note in § 5
Week 2.**

### If Matt Lesson Moves Off the Planned Day

Sunday mock → writing essay becomes the lesson material.
Review it the evening before → bring to the lesson.

---

## 7. Sunday Full Mock Protocol

Total time: approximately 3–3.5 hours.

### Exam Sections (in order)

**1. Listening** (50 min including transfer)
- Use a Cambridge test not yet fully practised
- Apply differentiating keyword method throughout
- Use break time between sections to read ahead — do not check previous answers

**2. Reading** (60 min)
- Maintain pace — do not over-verify unless time remains
- Aim to finish all questions in time

**3. Writing** (60 min)
- Task 1: 20 min (letter)
- Task 2: 40 min (essay — skeleton first, then write continuously)

**4. Speaking — self-record** (15 min)
- Part 1: ~4 min (3–4 questions)
- Part 2: 1 min prep + 2 min talk
- Part 3: ~4 min (2–3 questions)
- Save: `03_speaking/self-practice/mock_YYYY-MM-DD.m4a`

### Error Analysis (30–45 min)

**Listening:**
- Transcript analysis for S4 (priority)
- Classify every S4 error using categories from `connie_profile.md` §7.5

**Writing:**
- Error scan: G001, G003, G010, G011 + note any new errors
- Note any error appearing for the second time this sprint

**Speaking (optional):**
- Listen back, note any hesitations or grammar errors

### What to Report to Me After

Tell me the following, and I will update all databases:

```
Listening: S1=X S2=X S3=X S4=X
S4 error categories: [list]
Writing Task 1: band estimate
Writing Task 2: band estimate, TR/CC/LR/GRA rough estimates
Writing errors found: [list]
Any error appearing 2nd time this sprint: [list]
Speaking notes (optional): [anything you noticed]
```

I will update: `listening_db.md` · `writing_db.md` · `connie_profile.md` Evidence Log · `dashboard.md`

---

## 8. Database Update Rules

| Trigger | Action | Who |
|---|---|---|
| Evening writing session done | Report errors found → I update DB | You report → I update |
| Evening listening session done | Report score + error categories → I update | You report → I update |
| Sunday mock done | Report all scores + error scan → I update all DBs | You report → I update |
| Joe lesson done | Write lesson notes → I extract patterns | You write → I extract |
| Matt lesson done | Write lesson notes → I extract patterns | You write → I extract |
| Grammar error appears 2nd time | Tell me → I add to `errors/grammar_db.md` as Low | You flag → I add |
| Same error 3rd+ time | I upgrade to Medium/High confidence | Automatic |

**Policy:**
- First occurrence of new error: note it, do not add to DB
- Second occurrence: tell me; I add as Low confidence
- Third+ occurrence: upgraded to Medium or High confidence

---

## 9. Saturday Buffer Rules

**If all week's tasks are complete:**
- Sprint retrospective questions only (30 min)
- No new content

**If tasks were missed, recover in this priority order:**
1. Wednesday writing (feeds directly into Matt lesson)
2. Tuesday listening (S4 data needed for pattern detection)
3. Monday writing (foundation for Wed)

Recover one missed session only. If more than one was missed, choose the highest priority and note the rest in the retrospective. Do not try to catch up everything on Saturday.

---

## 10. Sprint Retrospective Questions

Fill in on Sat 7/18 (or the first evening after the sprint ends).

### Method Check

| Question | Answer |
|---|---|
| Can I identify question type correctly before planning? | always / mostly / sometimes / no |
| Do I write the skeleton before every essay? | always / mostly / sometimes / forgot |
| Do my body paragraphs reach result/consequence level? | always / mostly / sometimes / no |
| Did I use transcript analysis after every S4 session? | both / once / skipped both |
| Did I avoid editing during drafting? | always / mostly / still editing |
| Did the weekly rhythm feel sustainable? | yes / mostly yes / too heavy / too light |

### Progress Check

| Measurable | Before Sprint | After Sprint |
|---|---|---|
| S4 score (most recent) | 5.1/10 avg | (fill in after Mock #2) |
| Most common S4 error type | unknown | (fill in after Tue sessions) |
| Body paragraph chain completion | Low | always / mostly / sometimes |
| Full timed essay completed | 0 | 1 (Wed 7/15) |

### Next Sprint Inputs

Check each that applies:

- [ ] Writing still too slow → more D3 full essays in Sprint-002
- [ ] Matt flagged Task 1 register → add Task 1 letters to Sprint-002
- [ ] Same S4 error type appeared twice → keep S4 as secondary target in Sprint-002
- [ ] Grammar error appeared 3+ times → add targeted drill to Sprint-002
- [ ] Joe flagged Part 2 stamina → add to Sprint-002 speaking target

---

## Sprint Measurables

| Item | Target | When |
|---|---|---|
| Task 2 question types classified | 6+ prompts | Mon W1, Fri W1, Mon W2 |
| Skeletons written | 3+ | Mon W1 (7/6), Fri W1 (7/10), Wed W2 |
| Body paragraphs with labeled sentence jobs | 4+ | Wed W1 (7/2 leftover essay), Mon W2 |
| Full essays completed (real deadlines, W1) | 2 | Mon W1 (7/6, due for 7/7), Fri W1 (7/10, due for 7/11) |
| Full timed essays (D3) | 1 | Wed W2 (7/15) |
| Cambridge S4 sections (standalone) | 2 | Tue W1, Tue W2 |
| Transcript analyses completed | 2+ | Tue W1, Tue W2 |
| Full mocks completed | 2 | Sun W1 (7/12), Sun W2 (7/19) |

---

## What NOT to Do This Sprint

| Avoid | Reason |
|---|---|
| Vocabulary drills | Matt + Joe: confirmed strength — not the bottleneck |
| Grammar workbooks | Log errors from own writing only |
| Extra Reading practice | Already at/above Band 7 target |
| IELTS social media content | Joe + Matt: explicitly warned against |
| Changing the method because it feels hard | Fluctuation ≠ failure — method needs 2 weeks to settle |
| Editing during drafting | Kills writing speed; review stage only |
| Skipping the skeleton | Non-negotiable, even under time pressure |
