# Organize Anki — Knowledge and Error Corrections

## Purpose

Convert active Vocabulary, Expression, Sentence Pattern, and approved Error
Correction notes into weekly Anki Front/Back cards, then archive only the source
notes that are confirmed to have an Anki card.

The active Knowledge Base folders act as an inbox. The archive folders remain part
of the Knowledge Base and continue to hold the canonical source notes.

## Triggers

Run this workflow when the user says any of:

- `整理 anki`
- `整理 Anki`
- `整理anki`

This direct command runs only this Anki workflow. It does not run the rest of
`weekly review`.

## Run Mode

- Direct `整理 anki`: the command counts as user approval for active Error
  Correction notes, so include them.
- Called inside `weekly review`: list pending Error Correction notes for the user
  to review, but do not export or archive them until the user directly says
  `整理 anki`.

## Input Folders

Scan Markdown files directly inside:

- `10_knowledge_base/expressions/`
- `10_knowledge_base/sentence_patterns/`
- `10_knowledge_base/vocabulary/`
- `10_knowledge_base/error_corrections/`

Exclude:

- `TEMPLATE.md`
- `README.md`
- everything already inside an `archive/` directory

Do not process Ideas, Grammar Notes, Writing methods, or any other Knowledge Base
category.

## Step 1 — Inventory and Validate

For every active source note:

1. read the complete note;
2. identify the exact Vocabulary headword, Expression, or Sentence Pattern target;
3. for Expressions and Sentence Patterns, confirm the note has a Function, Usage,
   and Example;
4. for Expressions, also read Common Collocations;
5. for Sentence Patterns, also read Structure.
6. for Vocabulary, confirm the note has a Front plus Word, Pronunciation, Part of
   Speech, Frequency, and at least two labelled Examples in the Back.
7. for Error Corrections, confirm the note has the exact original Front plus a
   Corrected Version, Error Analysis, Key Reminder, and Pending review metadata.

If a note lacks enough information for a useful card, leave it in the active folder
and report what is missing. Do not invent the missing knowledge merely to archive
the file.

## Step 2 — Search for Existing Cards

Before generating anything, search every Markdown file under `08_ai/anki/`, not
only the weekly folder.

For Vocabulary, Expressions, and Sentence Patterns, compare normalized targets
case-insensitively, ignoring Markdown emphasis, backticks, and insignificant
punctuation. A different example does not make the same target a new card.

For Error Corrections, compare the normalized complete original Front. A revised
analysis of the same original sentence is not a new card.

- If the exact target already has a card, do not generate a duplicate.
- Record the existing Anki file as Practice Evidence.
- The source note is eligible for archiving because its Anki destination is
  verified.

## Step 3 — Generate Front/Back Cards

Create cards from
[`TEMPLATE.md`](TEMPLATE.md).

### Expression card

```markdown
---

**Front:**

[An English situation describing the meaning, context, and intended effect. Ask
the learner to produce the expression without revealing it.]

**Back:**

**[Exact expression]**

Function: [Concise function.]

Example: [Existing natural example from the source note.]

Common collocations: [Two or three from the source note.]

Source: `[Final archive path]`
```

### Sentence Pattern card

```markdown
---

**Front:**

[An English IELTS situation describing where the pattern belongs, what position it
expresses, and what communicative job it performs. Ask the learner to produce the
pattern without revealing it.]

**Back:**

**[Exact sentence pattern]**

Structure: `[Reusable structure from the source note]`

Example: [Existing natural example from the source note.]

Source: `[Final archive path]`
```

### Vocabulary card

```markdown
---

**Front:**

[Exact English definition from the source note's Front]

**Back:**

**[Exact headword]**

Pronunciation: [IPA]

Part of speech: [part of speech]

Frequency: [sourced frequency statement or Not available]

Examples:

- **[Domain 1]:** [Example from the source note]
- **[Domain 2]:** [Example from the source note]

Source: `[Final archive path]`
```

### Error Correction card

```markdown
---

**Front:**

[Exact original Front, including its errors]

**Back:**

**Corrected version**

[Corrected Version from the source note]

**Error analysis**

[Complete concise Error Analysis from the source note]

**Key reminder**

[Key Reminder from the source note]

Source: `[Final archive path]`
```

Rules:

- Vocabulary, Expression, and Sentence Pattern Fronts and Backs are in English.
- Error Correction Fronts preserve the learner's English exactly. Keep the
  Corrected Version in English, but preserve Traditional Chinese for Error Analysis
  and Key Reminder.
- Do not create Chinese-to-English translation cards.
- Do not reveal the exact answer on the Front.
- Preserve the exact target on the Back.
- Use source-note definitions, examples, collocations, and metadata; do not add
  unsupported facts.
- Generate one card per canonical source note.

## Step 4 — Save Weekly Output

Save new cards to:

`08_ai/anki/weekly/knowledge-review_YYYY-MM-DD.md`

Use the current local date.

- If the file does not exist, create it from `TEMPLATE.md`.
- If it already exists, append only non-duplicate cards to the correct section.
- Keep Sentence Patterns under `## [Structure] Sentence Patterns`.
- Keep Expressions under `## [Expression] Collocations and Chunks`.
- Keep Vocabulary under `## [Vocabulary] Words`.
- Keep Error Corrections under `## [Error Correction] Original → Corrected`.
- If every target already exists in Anki, do not create an empty weekly file.

## Step 5 — Archive Confirmed Source Notes

Only after a new card has been written successfully, or an existing matching card
has been verified, move the source note to:

- `10_knowledge_base/expressions/archive/<original-filename>.md`
- `10_knowledge_base/sentence_patterns/archive/<original-filename>.md`
- `10_knowledge_base/vocabulary/archive/<original-filename>.md`
- `10_knowledge_base/error_corrections/archive/<original-filename>.md`

Never overwrite an archive file. If the destination already exists and is not
identical, stop for that item and report the conflict.

After each move:

1. update repo-relative links that pointed to the old source path;
2. update the corresponding Knowledge Review Queue link to the archive path;
3. keep the archived note searchable during all future Knowledge Base deduplication.

Do not archive:

- `TEMPLATE.md` or folder documentation;
- malformed or incomplete notes;
- a note whose card write failed;
- a note when neither a new card nor a verified existing card can be identified.

## Step 6 — Update Knowledge Review Queue

For every archived target, update
`09_coach/knowledge_review_queue.md`:

- Status → `Anki`
- Last Review → current local date
- Practice Evidence → link to the new or existing Anki file
- Knowledge link → final archive path

Legacy `Podcast` evidence may remain in Practice Evidence, but it does not prevent
Anki generation. When such an item receives an Anki card, its Status becomes
`Anki`, and both Podcast and Anki evidence may be retained.

If an active source note has no queue row, add one with its original Added date
when known; otherwise use the current date.

## Completion Report

Report:

- weekly Anki output path, or `No new Anki file was needed`;
- Error Corrections converted or awaiting review;
- Vocabulary converted;
- Expressions converted;
- Sentence Patterns converted;
- duplicates found in existing Anki files;
- source notes moved to each archive;
- source notes left active and why.

## Restrictions

- Do not process archived notes again.
- Do not generate duplicate Anki targets.
- Do not delete source notes; archive them.
- Do not archive before verifying Anki coverage.
- Do not export Error Corrections from an automatic `weekly review`; direct
  `整理 anki` approval is required.
- Do not update Podcast, Source Brief, Output Drill, Chant, Sprint, performance, or
  error files.
- Do not perform external research.
