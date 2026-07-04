# IELTS Knowledge Base — Index

> Reusable knowledge cards extracted from lessons, transcripts, and writing feedback.
>
> **2026-07-05 restructure:** old `writing/`, `expressions/`, `collocations/` card
> sets were merged into `writing/` (duplicated the same content in two places) —
> see the table below for where each old ID landed. `vocabulary/`, `listening/`,
> `speaking/` (plus `E004`) are simply other subfolders of this same knowledge
> base — they were never duplicated, just orphaned once Podcast generation stopped
> reading this index for card rotation. This index below only lists
> `grammar/`, `prepositions/`, `word_form/` — kept deliberately separate from
> `09_coach/errors/*.md` (different purpose: teaching-card format here vs
> confidence-tracked error evidence there). Everything — `ideas/`, `coaches/`,
> `consensus/`, `vocabulary/`, `listening/`, `speaking/`, `writing/`,
> `grammar/`, `prepositions/`, `word_form/` — now lives together under
> `10_knowledge_base/` as a single top-level knowledge folder.
>
> **Total cards indexed below:** 18 (was 37)
> **Last updated:** 2026-07-05
>
> Format: `[ID] Title — one-line description`

---

## Grammar (11 cards)

| ID | File | Description | Priority |
|---|---|---|---|
| G001 | [Past Tense Time Markers](grammar/G001_past_tense_time_markers.md) | Explicit past time markers force simple past (not present perfect) | 🔴 High |
| G002 | [Past Perfect + ago](grammar/G002_past_perfect_ago.md) | `ago` forces simple past — never use past perfect with `ago` | 🔴 High |
| G003 | [information Uncountable](grammar/G003_information_uncountable.md) | `information` is always uncountable — no `-s`, no `a` | 🔴 High |
| G004 | [Uncountable Nouns Group](grammar/G004_uncountable_nouns_group.md) | `feedback`, `advice`, `staff`, `equipment` — all uncountable | 🟡 Medium |
| G005 | [Subject-Verb Agreement](grammar/G005_subject_verb_agreement.md) | `there are`, plural subjects, `each` → singular | 🟡 Medium |
| G006 | [Third-Person Singular](grammar/G006_third_person_singular.md) | `she/he/it` + verb-s / has in present simple | 🔴 High |
| G007 | [Compound Subject Pronoun](grammar/G007_compound_subject_pronoun.md) | `my sister and I` (not `me`) as subject | 🟡 Medium |
| G008 | [Modal Bare Infinitive](grammar/G008_modal_bare_infinitive.md) | Modal verbs + bare infinitive; `end up` + gerund | 🟡 Medium |
| G009 | [Past Passive](grammar/G009_past_passive.md) | `was/were + past participle` — auxiliary is required | 🟡 Medium |
| G010 | [Double Conjunction](grammar/G010_double_conjunction.md) | `Although` and `However` cannot coexist in one sentence | 🔴 **Critical** |
| G011 | [due to + Clause](grammar/G011_due_to_clause.md) | `due to` takes noun phrase only — use `because` for clauses | 🔴 High |

---

## Prepositions (4 cards)

| ID | File | Description | Priority |
|---|---|---|---|
| P001 | [listen to](prepositions/P001_listen_to.md) | `listen` requires `to` — it is not transitive | 🔴 High |
| P002 | [on the other hand](prepositions/P002_on_the_other_hand.md) | Fixed phrase — `in another hand` does not exist | 🔴 High |
| P003 | [on social media](prepositions/P003_on_social_media.md) | Platforms use `on` — `in social medium` is wrong | 🔴 High |
| P004 | [request + as a result of](prepositions/P004_request_and_as_a_result.md) | `request` (no `for`); `as a result of` (not `in a result of`) | 🟡 Medium |

---

## Word Form (3 cards)

| ID | File | Description | Priority |
|---|---|---|---|
| W001 | [-ed vs -ing Adjectives](word_form/W001_ed_vs_ing_adjectives.md) | `-ed` = how a person feels; `-ing` = what causes the feeling | 🟡 Medium |
| W002 | [Predicative Adjective](word_form/W002_predicative_adjective.md) | `make it easy` (not `easily`) — adjective after `make/find/consider it` | 🟡 Medium |
| W003 | [Noun vs Adjective in Compounds](word_form/W003_noun_adj_compound.md) | `loyal customer` (not `loyalty customer`); nationality adjectives | 🟡 Medium |

---

## Priority Key

| Symbol | Meaning |
|---|---|
| 🔴 Critical | Must know before every writing/speaking session |
| 🔴 High | Recurring personal errors or high-frequency patterns |
| 🟡 Medium | Important but not daily urgency |

---

## Moved / Merged Content (2026-07-05)

Don't look for these here anymore:

| Was here | Now at |
|---|---|
| `writing/WR001`–`WR008` | Merged into [`writing/writing_patterns.md`](writing/writing_patterns.md) (§1–10) |
| `expressions/E001`, `E002`, `E003` | Merged into [`writing/expressions.md`](writing/expressions.md) and [`writing/sentence_patterns.md`](writing/sentence_patterns.md) |
| `collocations/C001` | Merged into [`writing/expressions.md`](writing/expressions.md) § Natural Collocations |
| `expressions/E004` (Part 3 openers — this was Speaking content, not Writing) | Moved to [`speaking/E004_part3_opinion_openers.md`](speaking/E004_part3_opinion_openers.md) |
| `vocabulary/V001`, `V002` | Moved to [`vocabulary/`](vocabulary/) |
| `listening/L001`–`L005` | Moved to [`listening/`](listening/) |
| `speaking/SP001`–`SP004` | Moved to [`speaking/`](speaking/) |

---

## How to Use This Knowledge Base

### For NotebookLM
Upload all `.md` files in `10_knowledge_base/` as a source (now grammar/prepositions/
word_form only). Ask NotebookLM to generate a quiz or explain a rule as a podcast.

### For Self-Study
Start with all 🔴 Critical cards. Then move through High → Medium by category.

---

## Adding New Cards

Follow the card format in each existing file. After adding:
1. Add a row to this index
2. Update the Total cards count
3. Link related cards in the `## Related Knowledge` section
