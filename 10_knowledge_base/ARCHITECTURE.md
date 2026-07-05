# Knowledge Base Architecture

> Last updated: 2026-07-05

## Purpose

`10_knowledge_base/` stores IELTS knowledge that Connie can reuse repeatedly.

It does not store learning workflows, NotebookLM Source Briefs, legacy Podcast
Episode Packages, lesson transcripts, or one-off practice output. Those belong to
their own systems.

## The nine categories

```text
10_knowledge_base/
├── expressions/          # Collocations, chunks, fixed phrases, and useful words
├── sentence_patterns/    # Reusable sentence frames with replaceable slots
├── ideas/                # Reusable IELTS arguments, not English wording
├── grammar_notes/        # Connie's recurring grammar and usage errors
├── writing/              # Writing methods, skeletons, and paragraph frameworks
├── coaches/              # Distilled teaching knowledge from individual coaches
├── consensus/            # Principles shared across coaches
├── listening/            # Reusable listening techniques
└── speaking/             # Reusable speaking structures and techniques
```

## Classification rule

Ask what kind of reusable knowledge the item is:

1. A fixed chunk that drops into many sentences almost unchanged?
   → `expressions/`
2. A sentence frame with replaceable content?
   → `sentence_patterns/`
3. An argument or viewpoint rather than English wording?
   → `ideas/`
4. A recurring personal grammar or usage error?
   → `grammar_notes/`
5. A reusable method for one IELTS skill?
   → `writing/`, `listening/`, or `speaking/`
6. A principle attributable to one teacher?
   → `coaches/`
7. A principle supported by multiple teachers?
   → `consensus/`

Single words do not need a separate `vocabulary/` category. If a word is worth
retaining as reusable language, store it with expressions.

## Boundaries

- `07_podcast/` generates source-grounded NotebookLM briefs in Stage 1,
  ElevenLabs-ready Output Drills in Stage 2, and pattern-memory chants in Stage 3
  after required user input passes each gate. No stage reads the Knowledge Base
  automatically; a Knowledge Base note may be used only when the user explicitly
  supplies or selects it.
- Learning schedules, sprints, dashboards, and practice methods belong to the
  coaching/process layer.
- Full essays and spoken answers are applications of knowledge, not Knowledge Base
  entries.
- Legacy Podcast episodes and one-off briefing articles remain outside the
  Knowledge Base.

## Source of truth

Each reusable item should have one canonical home. Other systems link to it rather
than copying it. Ideas should remain atomic where practical: one reusable argument
per note.

## Update workflow

Treat the Knowledge Base as a curated database, not a notebook.

1. Extract the reusable element; do not save the whole source sentence by default.
2. Search the full Knowledge Base before writing.
3. Prefer enriching or merging an existing entry.
4. Create a new Markdown file only for a genuinely new concept.
5. Classify it into one of the nine categories above.
6. Never route an entry into Stage 1, Stage 2, or Stage 3 automatically.
7. Check related links and repository documentation before finishing.

New Expression and Sentence Pattern entries are also added to
`09_coach/knowledge_review_queue.md`. This is process state, not reusable knowledge,
so it remains outside the Knowledge Base. Weekly review routes high-value items to
`08_ai/anki/weekly/`; it does not send them into the Source Brief workflow.

## Entry formats

Expressions and sentence patterns use one reusable item per Markdown file. Do not
keep a single aggregate database file in either folder. Start from the relevant
`TEMPLATE.md`.

An Expression entry contains:

```text
## Expression
### Function
### Usage
### Common Collocations
### Example
### IELTS Topics
```

A Sentence Pattern entry contains:

```text
## Sentence Pattern
### Function
### Structure
### Usage
### Example
### IELTS Topics
```

Do not save Chinese translations unless Connie explicitly requests them. Prefer
reusable English over isolated vocabulary and lesson-summary prose.

## Possible future category

Do not add this yet. Once there is enough successful personal output, consider:

```text
usage/
├── writing_examples/
└── speaking_examples/
```

This would contain examples that Connie used successfully and that a coach explicitly
validated. Until then, successful output stays in its original Writing or Speaking
record.
