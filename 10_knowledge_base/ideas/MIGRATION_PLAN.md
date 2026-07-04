# Ideas Migration Plan

> Status: **Completed 2026-07-04.** All 6 ideas from `10_knowledge_base/writing/ideas.md`
> have been migrated into atomic notes below; the original file has been deleted.
> This file is kept as the historical record of what moved where, and as a scan log
> for other repo content that was considered and deliberately NOT migrated.
> Last updated: 2026-07-04

---

## 1. Repo-wide scan for reusable-idea content

| File | Contains | Migration decision |
|---|---|---|
| `10_knowledge_base/writing/ideas.md` | 6 fully-formed reusable ideas (Democratisation of Access, Commodification of Culture, Short-Term Stake/Irresponsible Behaviour, Job Creation ≠ Job Quality, Profit Leakage, Individually Harmless Collectively Damaging), all sourced from the International Tourism model essay (2026-07-02) | **Migrated** — see §2. File deleted after migration. |
| `02_writing/task2/models/international-tourism_model_2026-07-02.md` | Source essay for the 6 ideas above | Untouched — remains the evidentiary source, referenced from each note's `Related Notes` field |
| `02_writing/task2/models/print-vs-digital_model_2026-06-19.md`, `language-loss_model_2026-06-26.md`, `skills-vs-facts_model_2026-07-01.md` | Each model essay likely has 1–3 arguable "ideas" never extracted (only the tourism essay had been mined) | **Not migrated** — extracting a "reusable idea" out of free-form essay prose requires editorial judgment (does it really pass the "still usable in 3+ topics in 6 months" test?) that shouldn't be done as a blind bulk pass. Mine opportunistically next time each topic resurfaces, via `萃取知識`. |
| `10_knowledge_base/writing/writing_patterns.md` §8 "Common Argument Frameworks" (Individual vs Society, Short-term vs Long-term, Economic vs Environmental, Government vs Individual, Developed vs Developing) | Argument **lenses/dimensions**, not standalone ideas — no Why/Example/Development of their own | **Not migrated** — stays a Writing Pattern. These are categories an idea might use, not ideas themselves. |
| `10_knowledge_base/writing/writing_patterns.md` §9 "Common Task 2 Topics" | Topic-awareness list (which topics exist), not arguments | **Not migrated** — no idea content, it's a topic map |
| `10_knowledge_base/writing/skeletons.md`, `skeleton_*.md`, `sentence_patterns.md`, `expressions.md` | Structure templates and language chunks | **Not migrated** — different knowledge type (Writing Patterns / Sentence Patterns / Expressions), already correctly separated per `CLAUDE.md`'s 萃取知識 classification |
| `10_knowledge_base/*` (grammar/expressions/collocations/word_form/listening/speaking cards) | Language and skill drill cards for the Podcast card-rotation system | **Not migrated** — different system, not IELTS argument content |
| `03_speaking/speaking_notes.md`, `02_writing/writing_notes.md`, `01_lessons/teacher.md` | Coaching principles and technique notes | **Not migrated** — Teacher Principles, not Ideas |
| `09_coach/*`, `06_error_database/*`, `04_listening/*`, `05_reading/*` | Performance data, error patterns, skill drills | **Not migrated** — no reusable argument content found |

---

## 2. Migrated atomic idea notes

| Former entry in `ideas.md` | New file | Theme |
|---|---|---|
| Democratisation of Access | `technology-ai/access-to-goods-and-services-has-become-democratised.md` | technology-ai (cross-applies: education, culture-tourism, health) |
| Commodification of Culture | `culture-tourism/commercialisation-erodes-cultural-authenticity.md` | culture-tourism (cross-applies: government-society, technology-ai) |
| Short-Term Stake, Irresponsible Behaviour | `government-society/no-long-term-stake-leads-to-irresponsible-behaviour.md` | government-society (cross-applies: environment, work-career, family-children) |
| Job Creation ≠ Job Quality | `work-career/job-creation-does-not-guarantee-job-quality.md` | work-career (cross-applies: technology-ai, government-society) |
| Profit Leakage | `culture-tourism/profit-leakage-limits-local-economic-benefit.md` | culture-tourism (cross-applies: government-society, work-career) |
| Individually Harmless, Collectively Damaging | `environment/small-individual-actions-cause-large-collective-harm.md` | environment (cross-applies: technology-ai, health) |

Each note added a genuinely new **Speaking Use** section — the old `ideas.md` format
had no Speaking angle, only `Development` (a Writing body-paragraph chain). The
`Writing Use` section in each new note reuses that original `Development` field.

Ideas that legitimately apply to more than one theme are **not duplicated** across
folders — the file lives once, under its primary theme, and other applicable themes
are listed in that note's `Related Notes` section.

---

## 3. What replaced the old file

- `10_knowledge_base/writing/ideas.md` — **deleted**. All 6 entries migrated; no content lost.
- `CLAUDE.md` — the 萃取知識行為 (Step 2 classification table and file tree) updated
  to point Reusable Ideas storage at `10_knowledge_base/ideas/<theme>/` instead of the old path.
  (Correction from an earlier draft of this plan: it is the `萃取知識` behavior, not
  `存範本`, that governs where new Reusable Ideas get written — `存範本` only writes
  Band estimate / good-points / expressions / sentence-pattern blocks, and updates
  `sentence_patterns.md` and `skeleton_*.md`, never `ideas.md`.)

---

## 4. Avoiding duplication going forward

1. Before creating a new idea note, search `10_knowledge_base/ideas/<theme>/` for an existing
   note with an overlapping `Core Idea` — if the claim is materially the same, extend
   the existing note's `Related Notes` instead of creating a new file.
2. `10_knowledge_base/ideas/INDEX.md`'s "Idea Index by Theme" is the single lookup table —
   update it whenever a new idea note is added.
3. `CLAUDE.md`'s 萃取知識行為 now writes new Reusable Ideas straight to
   `10_knowledge_base/ideas/<theme>/`, using `10_knowledge_base/ideas/TEMPLATE.md`'s format — there is
   no longer a second path where an idea could land.
