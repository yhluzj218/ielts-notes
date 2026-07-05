# Vocabulary Intake Workflow

## Purpose

Turn one user-selected English word into a source-backed Front/Back vocabulary note
in the Knowledge Base. Do not create an Anki card during intake.

Vocabulary notes enter the active inbox first. The separate `整理 anki` workflow
converts them into Anki cards during weekly organization and then moves confirmed
source notes to `10_knowledge_base/vocabulary/archive/`.

## Triggers

Run this workflow when the user:

- says `收錄單字 [word]`;
- says `學單字 [word]`;
- says `[word] 做成單字卡`;
- provides one English headword as the whole request while working in this
  vocabulary workflow.

If the input is a multi-word chunk or sentence frame, do not force it into
Vocabulary. Route a fixed chunk to Expressions and a replaceable frame to Sentence
Patterns.

## Required Input

- exactly one user-selected English headword.

Do not choose a word for the user.

## Source Resolution

1. Open `https://www.vocabulary.com/dictionary/<word>` first.
2. Use Vocabulary.com for pronunciation, part of speech, word forms, and meaning
   when those fields are visible.
3. Paraphrase the definition into one concise English Front. Do not copy the site's
   explanatory article or example corpus.
4. Create two short original examples with useful domain labels such as Business,
   Science, Education, Society, Technology, or Environment.
5. If the user supplies examples, preserve them when correct and mark them as
   user-provided.
6. Record an exact frequency statement only when Vocabulary.com visibly provides
   it or the user supplies it. Otherwise write `Not available from the consulted
   source.` Do not estimate.
7. If Vocabulary.com is unavailable or lacks a required field, use a reputable
   dictionary fallback and record the exact source. Mark unresolved fields
   `Not available`; never invent them.

## Deduplication

Before creating a note, search:

- `10_knowledge_base/vocabulary/`;
- `10_knowledge_base/vocabulary/archive/`;
- all files under `08_ai/anki/`.

Compare headwords case-insensitively.

- If an active note exists, improve that note instead of creating another.
- If an archived note exists, update it only when the user provides useful new
  evidence; do not move it back to active automatically.
- If an Anki card exists but no Knowledge note exists, create the Knowledge note
  directly in `archive/` and link the existing Anki evidence in the queue.

## Knowledge Note Format

Start from:

`10_knowledge_base/vocabulary/TEMPLATE.md`

Required fields:

```markdown
# Vocabulary — [word]

## Front

[Concise English definition without the target word]

## Back

### Word

**[word]**

### Pronunciation

[IPA]

### Part of Speech

[part of speech]

### Frequency

[Exact sourced statement or Not available]

### Examples

- **[Domain 1]:** [Natural example]
- **[Domain 2]:** [Natural example]

### Other Forms

- [form]

## Source

- Dictionary: [source]
- URL: [direct source URL]
- Accessed: YYYY-MM-DD
- Notes: [which fields came from the source or user]
```

The Front must not contain the answer or a transparent form of it.

## Storage

Save a new, not-yet-exported note to:

`10_knowledge_base/vocabulary/<word-slug>.md`

If that path exists, update it rather than creating `-02`.

Add or update one row in:

`09_coach/knowledge_review_queue.md`

Use Type `Vocabulary` and Status `Pending`. Link the Knowledge field to the active
note.

## Completion Report

Report:

- saved Knowledge note;
- source used;
- fields unavailable or supplied by the user;
- queue status;
- explicit confirmation that no Anki file was created.

## Restrictions

- Do not choose a word.
- Do not write directly to `08_ai/anki/` during intake.
- Do not archive a new note during intake unless a matching Anki card already
  exists.
- Do not copy long dictionary explanations or third-party example corpora.
- Do not invent pronunciation, part of speech, frequency, or usage evidence.
- Do not update Podcast, Sprint, performance, or error files.
