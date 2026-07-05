# Knowledge Base Architecture

> Last updated: 2026-07-05

## Purpose

`10_knowledge_base/` stores IELTS knowledge that Connie can reuse repeatedly.

It does not store learning workflows, NotebookLM Source Briefs, legacy Podcast
Episode Packages, lesson transcripts, or one-off practice output. Those belong to
their own systems.

## The eleven categories

```text
10_knowledge_base/
├── vocabulary/           # User-selected single headwords waiting for Anki
│   └── archive/          # Canonical Vocabulary notes with verified Anki coverage
├── expressions/          # Active Anki inbox for chunks and fixed phrases
│   └── archive/          # Canonical Expression notes with verified Anki coverage
├── sentence_patterns/    # Active Anki inbox for reusable sentence frames
│   └── archive/          # Canonical Pattern notes with verified Anki coverage
├── error_corrections/    # Exact learner sentences with corrections and analysis
│   └── archive/          # Reviewed corrections with verified Anki coverage
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

1. A user-selected single English headword?
   → `vocabulary/`
2. A fixed chunk that drops into many sentences almost unchanged?
   → `expressions/`
3. A sentence frame with replaceable content?
   → `sentence_patterns/`
4. A complete sentence the learner wrote incorrectly, with its correction?
   → `error_corrections/`
5. An argument or viewpoint rather than English wording?
   → `ideas/`
6. A recurring personal grammar or usage error?
   → `grammar_notes/`
7. A reusable method for one IELTS skill?
   → `writing/`, `listening/`, or `speaking/`
8. A principle attributable to one teacher?
   → `coaches/`
9. A principle supported by multiple teachers?
   → `consensus/`

Vocabulary is deliberately user-selected. Do not recommend or automatically collect
more advanced words merely to expand this folder. Multi-word chunks still belong in
Expressions.

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
2. Search the full Knowledge Base, including all four archive folders, before
   writing.
3. Prefer enriching or merging an existing entry.
4. Create a new Markdown file only for a genuinely new concept.
5. Classify it into one of the eleven categories above.
6. Never route an entry into Stage 1, Stage 2, or Stage 3 automatically.
7. Check related links and repository documentation before finishing.

New Vocabulary, Expression, Sentence Pattern, and Error Correction entries are also added to
`09_coach/knowledge_review_queue.md`. This is process state, not reusable knowledge,
so it remains outside the Knowledge Base.

Vocabulary, Expression, Sentence Pattern, and Error Correction root folders are
active review/Anki inboxes.
The direct `整理 anki` command and `weekly review` both run
`08_ai/anki/weekly/organize_anki_workflow.md`. After a new card is written—or a
matching existing card is verified—the canonical source note moves to its
category's `archive/`. Error Corrections additionally require direct user approval
through `整理 anki`; an automatic `weekly review` only lists them. Archive notes
remain searchable Knowledge Base sources but
are not processed into Anki again. A failed or incomplete item stays active.

This Anki workflow does not send anything into the Source Brief workflow.

## Entry formats

Vocabulary, expressions, sentence patterns, and error corrections use one item per
Markdown file. Do not keep a single aggregate database file in these folders. Start
from the relevant `TEMPLATE.md`. New notes begin in the category root; do not create
them directly in `archive/`.

A Vocabulary entry contains:

```text
## Front
## Back
### Word
### Pronunciation
### Part of Speech
### Frequency
### Examples
### Other Forms
## Source
```

Vocabulary intake is defined by
`08_ai/anki/vocabulary_intake_workflow.md`. It prefers Vocabulary.com, records the
direct source, never invents frequency, and does not write to Anki during intake.

An Error Correction entry contains:

```text
## Front
## Back
### Corrected Version
### Error Analysis
### Key Reminder
## Metadata
```

Error Correction intake is defined by
`08_ai/anki/error_correction_intake_workflow.md`. It preserves the original Front
exactly, keeps the correction and analysis together on one Back, and never creates
other language notes as a side effect.

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
reusable English and user-selected words over automatically collected vocabulary or
lesson-summary prose.

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
