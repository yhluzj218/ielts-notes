# Error Correction Intake Workflow

## Purpose

Save one complete learner sentence or short response as a simple correction card:

- Front = the learner's exact original wording;
- Back = the best corrected version plus the AI's error analysis.

The card enters the Knowledge Base for human review. It does not enter Anki during
intake.

## Triggers

Run this workflow when the user says:

- `記錄造句錯誤`;
- `收錄造句錯誤`;
- `記錄這個錯誤`;
- `把這個錯誤留到 Anki`.

## Input

Accept:

- the learner's original sentence or short response;
- an existing suggested correction, if supplied;
- existing AI or teacher analysis, if supplied;
- the learner's intended meaning, if needed.

If no correction is supplied, produce one that preserves the intended meaning.
If the intended meaning is genuinely ambiguous, ask before saving.

## Card Design

Use:

`10_knowledge_base/error_corrections/TEMPLATE.md`

Required structure:

```markdown
# Error Correction — [short label]

## Front

[Exact original sentence, including its errors]

## Back

### Corrected Version

[Best natural correction]

### Error Analysis

1. **[Problem]** — [Concise explanation and better choice.]
2. ...

### Key Reminder

[One short transferable reminder.]

## Metadata

- Date: YYYY-MM-DD
- Skill: Writing / Speaking
- Topic: [topic or Unknown]
- Review Status: Pending
- Source: User sentence and supplied AI/teacher feedback
```

Rules:

- Preserve the Front exactly. Do not silently fix spelling, punctuation, or
  capitalization there.
- Put the corrected English before the analysis on the Back.
- Keep all analysis for that original sentence on one card.
- Write `Error Analysis` and `Key Reminder` in Traditional Chinese. Keep the
  original Front and Corrected Version in English.
- Do not split one sentence into separate cards.
- Do not create Vocabulary, Expression, Sentence Pattern, or Idea notes as a side
  effect.
- Do not add every issue to the machine Error DB. Existing recurrence/confidence
  rules still apply independently.

## Deduplication

Search:

- `10_knowledge_base/error_corrections/`;
- `10_knowledge_base/error_corrections/archive/`;
- all existing files under `08_ai/anki/`.

Use the normalized original Front as the identity. If the same original already
exists, improve its Back rather than creating a duplicate.

## Storage

Save to:

`10_knowledge_base/error_corrections/YYYY-MM-DD_<short-slug>.md`

If an unrelated card already uses the path, append `-02`, `-03`, and so on.

Add one row to:

`09_coach/knowledge_review_queue.md`

Use Type `Error Correction`, Status `Pending`, and link to the active Knowledge
note.

## Review and Anki Boundary

Intake creates only the Knowledge note and queue row.

The direct command `整理 anki` means the user has reviewed and approved active
Error Correction cards. It may then create their Anki cards and archive the source
notes.

When `weekly review` runs without the direct `整理 anki` command, list pending Error
Correction notes for review but do not export or archive them yet.

## Completion Report

Report:

- saved Knowledge note;
- original Front;
- corrected version;
- queue status;
- confirmation that no Anki file or other Knowledge category was created.

## Restrictions

- Do not rewrite the Front.
- Do not create extra language cards.
- Do not write directly to Anki during intake.
- Do not archive before direct user approval through `整理 anki`.
- Do not perform external research.
