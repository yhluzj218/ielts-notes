# Knowledge Review Queue

> Process-layer queue for routing new Expressions and Sentence Patterns into
> weekly Anki generation. The reusable knowledge itself remains in
> `10_knowledge_base/`; this file stores workflow state only. Phase 1 NotebookLM
> Source Brief generation does not read or update this queue.

## Status values

- `Pending` — waiting for the first weekly review
- `Podcast` — legacy status from a superseded workflow; preserve as history
- `Rollover` — legacy waiting status; route at the next weekly review
- `Anki` — an Anki card has been generated
- `Merged` — merged into another Knowledge Base entry
- `Dropped` — not valuable enough for either practice channel

## Queue

| Added | Knowledge | Type | Status | Last Review | Practice Evidence |
|---|---|---|---|---|---|
| 2026-07-04 | [be packaged for consumption](../10_knowledge_base/expressions/be-packaged-for-consumption.md) | Expression | Pending | — | — |
| 2026-07-04 | [be retained within the local economy](../10_knowledge_base/expressions/be-retained-within-the-local-economy.md) | Expression | Pending | — | — |
| 2026-07-04 | [be severely damaged](../10_knowledge_base/expressions/be-severely-damaged.md) | Expression | Pending | — | — |
| 2026-07-04 | [be the preserve of](../10_knowledge_base/expressions/be-the-preserve-of.md) | Expression | Pending | — | — |
| 2026-07-04 | [be unevenly distributed](../10_knowledge_base/expressions/be-unevenly-distributed.md) | Expression | Pending | — | — |
| 2026-07-04 | [both tourists and host countries](../10_knowledge_base/expressions/both-tourists-and-host-countries.md) | Expression | Pending | — | — |
| 2026-07-04 | [contribute to greenhouse gas emissions](../10_knowledge_base/expressions/contribute-to-greenhouse-gas-emissions.md) | Expression | Pending | — | — |
| 2026-07-04 | [damage inflicted on](../10_knowledge_base/expressions/damage-inflicted-on.md) | Expression | Pending | — | — |
| 2026-07-04 | [have a greater awareness of](../10_knowledge_base/expressions/have-a-greater-awareness-of.md) | Expression | Podcast | 2026-07-04 | [S01E01](../07_podcast/episodes/season_01/ep01_sustainable-tourism-luxury.md) |
| 2026-07-04 | [multinational corporations](../10_knowledge_base/expressions/multinational-corporations.md) | Expression | Podcast | 2026-07-04 | [S01E01](../07_podcast/episodes/season_01/ep01_sustainable-tourism-luxury.md) |
| 2026-07-04 | [precarious employment](../10_knowledge_base/expressions/precarious-employment.md) | Expression | Pending | — | — |
| 2026-07-04 | [the less well-off](../10_knowledge_base/expressions/the-less-well-off.md) | Expression | Podcast | 2026-07-04 | [S01E01](../07_podcast/episodes/season_01/ep01_sustainable-tourism-luxury.md) |
| 2026-07-04 | [Although X does Y, limitation](../10_knowledge_base/sentence_patterns/although-x-does-y-limitation.md) | Sentence Pattern | Podcast | 2026-07-04 | [S01E01](../07_podcast/episodes/season_01/ep01_sustainable-tourism-luxury.md) |
| 2026-07-04 | [Despite advantages, these do not compensate for costs](../10_knowledge_base/sentence_patterns/despite-advantages-do-not-compensate-for-costs.md) | Sentence Pattern | Pending | — | — |
| 2026-07-04 | [From exclusive to accessible](../10_knowledge_base/sentence_patterns/from-exclusive-to-accessible.md) | Sentence Pattern | Pending | — | — |
| 2026-07-04 | [Related to this is the fact that](../10_knowledge_base/sentence_patterns/related-to-this-is-the-fact-that.md) | Sentence Pattern | Pending | — | — |
| 2026-07-04 | [Than was the case](../10_knowledge_base/sentence_patterns/than-was-the-case.md) | Sentence Pattern | Pending | — | — |
| 2026-07-04 | [There are, however, drawbacks associated with](../10_knowledge_base/sentence_patterns/there-are-however-drawbacks-associated-with.md) | Sentence Pattern | Pending | — | — |
| 2026-07-04 | [There are undoubtedly benefits flowing from](../10_knowledge_base/sentence_patterns/there-are-undoubtedly-benefits-flowing-from.md) | Sentence Pattern | Pending | — | — |
| 2026-07-04 | [Uneven distribution: minority versus majority](../10_knowledge_base/sentence_patterns/uneven-distribution-minority-majority.md) | Sentence Pattern | Pending | — | — |

## Weekly routing rules

1. Review every `Pending` or legacy `Rollover` item.
2. If it is valuable for active recall, generate an Anki card and mark it `Anki`.
3. Search all existing cards before generation; do not duplicate a target.
4. Merge or drop weak and duplicate knowledge instead of sending it to Anki.
5. Preserve existing `Podcast` rows as historical evidence; do not create new ones.
6. Do not route any item into NotebookLM Source Brief generation automatically.
