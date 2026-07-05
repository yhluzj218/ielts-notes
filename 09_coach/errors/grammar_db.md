# Grammar Error Database

> Machine-readable. Every entry must have evidence.
> Claude must check this file before flagging any grammar issue.
> Do not add new entries from a single observation — wait for a second occurrence.

---

## Schema

| Field | Description |
|---|---|
| ID | Unique ID (G001, G002…) |
| Category | tense · number · article · conjunction · verb-form · pronoun |
| Pattern | One-line description of the error rule |
| Error → Correct | Minimal example pair |
| Skills | writing · speaking · both |
| Confidence | High (3+ occurrences) / Medium (2) / Low (1) |
| First Seen | Approximate date |
| Count | Times observed |
| Status | Active / Resolved |
| Evidence | Source file(s) |

---

## Tense Errors

### G001 — Past time marker + present perfect
- **Pattern:** Explicit past time marker forces simple past; present perfect is wrong
- **Error → Correct:** `last week I have purchased` → `last week I purchased`
- **Skills:** both
- **Confidence:** High
- **First Seen:** 2026-06-19
- **Count:** 3+
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md` · `01_lessons/writing/writing-lesson_2026-06-19.md`

### G002 — Past perfect conflict with past time marker
- **Pattern:** `built / was built` with `ago` — both are past; don't mix perfect aspect
- **Error → Correct:** `he has built it 40 years ago` → `he built it 40 years ago`
- **Skills:** speaking
- **Confidence:** High
- **First Seen:** 2026-06-01
- **Count:** 2+
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md`

---

## Countable / Uncountable Nouns

### G003 — `information` pluralised
- **Pattern:** `information` is always uncountable
- **Error → Correct:** `informations` → `information`
- **Skills:** both
- **Confidence:** High
- **First Seen:** 2026-06-19
- **Count:** 3+
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md`

### G004 — `feedback` treated as countable
- **Pattern:** `feedback` is uncountable; cannot take `a` or `-s`
- **Error → Correct:** `a short feedback` → `some feedback` / `a piece of feedback`
- **Skills:** writing
- **Confidence:** Medium
- **First Seen:** 2026-06-19
- **Count:** 2
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md`

### G005 — `staff` pluralised
- **Pattern:** `staff` is uncountable as a collective; use `staff member(s)` to count
- **Error → Correct:** `staffs` → `staff` / `staff members`
- **Skills:** writing
- **Confidence:** Medium
- **First Seen:** 2026-06-19
- **Count:** 2
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md`

---

## Subject-Verb Agreement

### G006 — Existential `there` with plural noun
- **Pattern:** `there is` must match the following noun number
- **Error → Correct:** `There is several reasons` → `There are several reasons`
- **Skills:** writing
- **Confidence:** Medium
- **First Seen:** 2026-06-19
- **Count:** 2
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md`

### G007 — Plural subject + singular verb
- **Pattern:** A plural subject takes the base verb or plural auxiliary form, not a third-person singular form
- **Error → Correct:** `families tends to` → `families tend to`; `these does` → `these do`
- **Skills:** writing
- **Confidence:** High
- **First Seen:** 2026-06-19
- **Count:** 4
- **Last Seen:** 2026-07-05
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md` · `10_knowledge_base/error_corrections/2026-07-05_modern-tourism-cultural-values.md` · `10_knowledge_base/error_corrections/2026-07-05_film-studios-hollywood-formulas.md`

### G008 — Third-person singular `-s` omitted in speech
- **Pattern:** `she / he / it` requires auxiliary `has` / verb + `-s`
- **Error → Correct:** `she have never` → `she has never`
- **Skills:** speaking
- **Confidence:** Medium
- **First Seen:** 2026-06-22
- **Count:** 2
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md` · `01_lessons/speaking/speaking-lesson_2026-06-22.md`

---

## Pronouns

### G009 — Subject pronoun in compound subject
- **Pattern:** `I` required as subject; `me` is object form
- **Error → Correct:** `my sister and me are` → `my sister and I were`
- **Skills:** speaking
- **Confidence:** Medium
- **First Seen:** 2026-06-08
- **Count:** 2
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md` · `01_lessons/speaking/speaking-lesson_2026-06-08.md`

---

## Conjunctions

### G010 — Double conjunction: `although` + `however`
- **Pattern:** `although` and `however` are both concession markers; never use both in the same sentence
- **Error → Correct:** `Although X, however Y` → `Although X, Y` OR `X. However, Y.`
- **Skills:** writing
- **Confidence:** High
- **First Seen:** 2026-06-19
- **Count:** 4+
- **Last Seen:** 2026-06-29
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md` · `01_lessons/writing/writing-lesson_2026-06-19.md` · skeleton practice 2026-06-29

### G011 — `due to` followed by a clause
- **Pattern:** `due to` takes a noun phrase, not a clause; use `because` or `due to the fact that` for clauses
- **Error → Correct:** `due to she was late` → `because she was late` / `due to the fact that she was late`
- **Skills:** writing
- **Confidence:** High
- **First Seen:** 2026-06-19
- **Count:** 3+
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md` · `01_lessons/writing/writing-lesson_2026-06-19.md`

---

## Verb Form

### G012 — Modal verb + inflected form
- **Pattern:** Modal verbs (`might`, `could`, `would`, etc.) take bare infinitive
- **Error → Correct:** `might ended up` → `might end up`
- **Skills:** writing
- **Confidence:** Medium
- **First Seen:** 2026-06-19
- **Count:** 2
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md`

### G013 — `end up` + infinitive instead of gerund
- **Pattern:** `end up` takes gerund (`-ing`), not infinitive
- **Error → Correct:** `end up go for work` → `end up working`
- **Skills:** writing
- **Confidence:** Medium
- **First Seen:** 2026-06-19
- **Count:** 2
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md`

### G014 — Past passive missing auxiliary
- **Pattern:** Past passive requires `was/were + past participle`
- **Error → Correct:** `we been separated` → `we were separated`
- **Skills:** both
- **Confidence:** Medium
- **First Seen:** 2026-06-19
- **Count:** 2
- **Status:** Active
- **Evidence:** `06_error_database/error_log.md`

---

## Resolved Errors

### G-R001 — Past tense in writing (general)
- **Status:** Resolved
- **Resolved:** 2026-06-23
- **Evidence:** Matt's feedback: "past tense was pretty good today, definitely better"

---

## Update Rules

- New entry requires at minimum 2 occurrences before being added.
- Count field must increment each time the error is observed.
- When an error is not observed for 4+ consecutive graded sessions → change Status to Resolved.
- If a Resolved error reappears → reactivate and note date.
- Each entry must link to at least one evidence file.
