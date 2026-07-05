# Knowledge Review Queue

> Process-layer queue for routing new Vocabulary, Expressions, Sentence Patterns,
> and reviewed Error Corrections into Anki generation. The reusable knowledge itself remains in
> `10_knowledge_base/`; this file stores workflow state only. Phase 1 NotebookLM
> Source Brief generation does not read or update this queue.

## Status values

- `Pending` — waiting for the first weekly review
- `Podcast` — legacy evidence; still eligible for Anki while its source note is active
- `Rollover` — legacy waiting status; route at the next weekly review
- `Anki` — an Anki card has been generated
- `Merged` — merged into another Knowledge Base entry
- `Dropped` — not valuable enough for either practice channel

## Queue

| Added | Knowledge | Type | Status | Last Review | Practice Evidence |
|---|---|---|---|---|---|
| 2026-07-05 | [excavate](../10_knowledge_base/vocabulary/excavate.md) | Vocabulary | Pending | — | — |
| 2026-07-05 | [rural areas](../10_knowledge_base/expressions/rural-areas.md) | Expression | Pending | — | — |
| 2026-07-05 | [Public resources distribution correction](../10_knowledge_base/error_corrections/2026-07-05_public-resources-distribution.md) | Error Correction | Pending | — | — |
| 2026-07-05 | [Modern tourism and cultural values correction](../10_knowledge_base/error_corrections/2026-07-05_modern-tourism-cultural-values.md) | Error Correction | Pending | — | — |
| 2026-07-05 | [Programming and AI prototypes correction](../10_knowledge_base/error_corrections/2026-07-05_programming-ai-prototypes.md) | Error Correction | Pending | — | — |
| 2026-07-05 | [Film studios and Hollywood formulas correction](../10_knowledge_base/error_corrections/2026-07-05_film-studios-hollywood-formulas.md) | Error Correction | Pending | — | — |
| 2026-07-05 | [Parents and flexible working hours correction](../10_knowledge_base/error_corrections/2026-07-05_parents-flexible-working-hours.md) | Error Correction | Pending | — | — |
| 2026-07-04 | [be packaged for consumption](../10_knowledge_base/expressions/archive/be-packaged-for-consumption.md) | Expression | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [be retained within the local economy](../10_knowledge_base/expressions/archive/be-retained-within-the-local-economy.md) | Expression | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [be severely damaged](../10_knowledge_base/expressions/archive/be-severely-damaged.md) | Expression | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [be the preserve of](../10_knowledge_base/expressions/archive/be-the-preserve-of.md) | Expression | Anki | 2026-07-05 | [Existing Anki](../08_ai/anki/writing/vocabulary-by-category_2026-07-01.md) |
| 2026-07-04 | [be unevenly distributed](../10_knowledge_base/expressions/archive/be-unevenly-distributed.md) | Expression | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [both tourists and host countries](../10_knowledge_base/expressions/archive/both-tourists-and-host-countries.md) | Expression | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [contribute to greenhouse gas emissions](../10_knowledge_base/expressions/archive/contribute-to-greenhouse-gas-emissions.md) | Expression | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [damage inflicted on](../10_knowledge_base/expressions/archive/damage-inflicted-on.md) | Expression | Anki | 2026-07-05 | [Existing Anki](../08_ai/anki/writing/vocabulary-by-category_2026-07-01.md) |
| 2026-07-04 | [have a greater awareness of](../10_knowledge_base/expressions/archive/have-a-greater-awareness-of.md) | Expression | Anki | 2026-07-05 | [S01E01](../07_podcast/episodes/season_01/ep01_sustainable-tourism-luxury.md) · [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [multinational corporations](../10_knowledge_base/expressions/archive/multinational-corporations.md) | Expression | Anki | 2026-07-05 | [S01E01](../07_podcast/episodes/season_01/ep01_sustainable-tourism-luxury.md) · [Existing Anki](../08_ai/anki/writing/vocabulary-by-category_2026-07-01.md) |
| 2026-07-04 | [precarious employment](../10_knowledge_base/expressions/archive/precarious-employment.md) | Expression | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [the less well-off](../10_knowledge_base/expressions/archive/the-less-well-off.md) | Expression | Anki | 2026-07-05 | [S01E01](../07_podcast/episodes/season_01/ep01_sustainable-tourism-luxury.md) · [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [Although X does Y, limitation](../10_knowledge_base/sentence_patterns/archive/although-x-does-y-limitation.md) | Sentence Pattern | Anki | 2026-07-05 | [S01E01](../07_podcast/episodes/season_01/ep01_sustainable-tourism-luxury.md) · [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [Despite advantages, these do not compensate for costs](../10_knowledge_base/sentence_patterns/archive/despite-advantages-do-not-compensate-for-costs.md) | Sentence Pattern | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [From exclusive to accessible](../10_knowledge_base/sentence_patterns/archive/from-exclusive-to-accessible.md) | Sentence Pattern | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [Related to this is the fact that](../10_knowledge_base/sentence_patterns/archive/related-to-this-is-the-fact-that.md) | Sentence Pattern | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [Than was the case](../10_knowledge_base/sentence_patterns/archive/than-was-the-case.md) | Sentence Pattern | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [There are, however, drawbacks associated with](../10_knowledge_base/sentence_patterns/archive/there-are-however-drawbacks-associated-with.md) | Sentence Pattern | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [There are undoubtedly benefits flowing from](../10_knowledge_base/sentence_patterns/archive/there-are-undoubtedly-benefits-flowing-from.md) | Sentence Pattern | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |
| 2026-07-04 | [Uneven distribution: minority versus majority](../10_knowledge_base/sentence_patterns/archive/uneven-distribution-minority-majority.md) | Sentence Pattern | Anki | 2026-07-05 | [Anki](../08_ai/anki/weekly/knowledge-review_2026-07-05.md) |

## Weekly routing rules

1. Run `08_ai/anki/weekly/organize_anki_workflow.md`.
2. Review complete notes directly inside the active Vocabulary, Expression,
   Sentence Pattern, and Error Correction folders; archived notes are not processed
   again.
3. If it is valuable for active recall, generate an Anki card and mark it `Anki`.
4. Search all existing cards before generation; do not duplicate a target.
5. After a new or existing card is verified, move the source note into its category's
   `archive/`, update the Knowledge link, and retain the Anki file as Practice
   Evidence.
6. A legacy `Podcast` row remains eligible for Anki. Preserve its Podcast link as
   additional Practice Evidence when changing the Status to `Anki`.
7. Merge or drop weak and duplicate knowledge instead of sending it to Anki.
8. Do not route any item into NotebookLM Source Brief generation automatically.
9. Error Correction notes require direct user approval through `整理 anki`.
   `weekly review` only lists them for review and does not export or archive them.
