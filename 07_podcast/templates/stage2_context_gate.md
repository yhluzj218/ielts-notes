# Stage 2 Output Drill — Gate and Context Resolution

> This file defines only the Stage 2 input gate and context-resolution behaviour.
> It does not define or expand the Output Drill Script format.

## Trigger

Apply this gate whenever `podcast_gated_router.md` selects Stage 2. A complete
request normally provides an input headed:

```markdown
# Output Drill Input
```

If the direct `產生 Output Drill Script` trigger has no input block, apply the
incomplete-input response. Do not trigger Stage 2 merely because a new Stage 1
source brief exists.

## Step 1 — Validate Required User Input

Required fields:

- `Topic` — one non-empty topic;
- `Core Pattern` — one non-empty pattern;
- `Model Sentence` — one non-empty sentence;
- `Vocabulary / Expressions` — three to five non-empty user-provided items.

Optional fields:

- `Practice Topics`;
- `NotebookLM Recap / Context`;
- `Source Brief File`.

Practice Topics may be blank. Do not infer or generate a missing required field. In
particular, a source brief
must never be used to choose the Core Pattern, Model Sentence, or Vocabulary /
Expressions.

If any required field is incomplete, stop before resolving context or generating a
script. Reply:

```text
Output drill input is incomplete.

Please provide:

# Output Drill Input

## Topic
...

## Core Pattern
...

## Model Sentence
...

## Vocabulary / Expressions
1.
2.
3.

## Practice Topics
1.
2.
```

## Step 2 — Resolve Context in Priority Order

Use exactly one context source. Record it for the completion report.

### Priority 1 — User-provided NotebookLM Recap / Context

If `NotebookLM Recap / Context` contains substantive text, use it. It may be:

- a NotebookLM recap;
- important points from a NotebookLM transcript;
- the user's own summary of the discussion.

Do not search for or merge in a source brief when this field is present.

Record:

```text
Context used:
User-provided NotebookLM Recap / Context
```

### Priority 2 — Explicit Source Brief File

If `Source Brief File` contains a path:

1. resolve it relative to the repo root;
2. confirm that the file exists under `07_podcast/source_briefs/`;
3. read its `Source Briefing Article`, `Viewpoints`, and `Discussion Recap`;
4. use those sections as Stage 2 context.

The Source Log may be consulted to understand evidence boundaries, but Stage 2 must
not repeat the research.

If the explicit path does not exist or is not a source brief, stop and ask the user
to correct the path. Do not silently substitute a different file.

Record:

```text
Context used:
07_podcast/source_briefs/[filename].md
```

### Priority 3 — Match by Topic

Use this priority only when Priority 1 and Priority 2 are absent.

Search Markdown files directly inside `07_podcast/source_briefs/`, excluding
`README.md`. Match the supplied Topic against:

1. an exact or normalised topic slug in the filename;
2. the `Source Briefing Article` title;
3. the `Topic`, `IELTS Question`, viewpoint titles, and substantive content;
4. close topic keywords and common variants, such as `international tourism`,
   `tourism`, and `travel`.

Compare case-insensitively and treat spaces, underscores, and hyphens as equivalent.
Do not use a weak single-keyword overlap when the rest of the file concerns a
different topic.

If there is exactly one reasonable match, use it. If two or more files are
plausible, do not rank one silently by recency. List the repo-relative candidate
paths and ask the user to select one; do not generate the script yet.

Record a unique match as:

```text
Context used:
07_podcast/source_briefs/[matched-filename].md
```

### Priority 4 — Latest Source Brief

Use this priority only when no clear topic match exists.

- If the directory contains exactly one source brief file, use it.
- If the user explicitly says `用最新的`, select the source brief with the latest
  modification time.
- If multiple files exist and the user did not explicitly request the latest,
  list their repo-relative paths and ask the user to choose. Do not guess.

Exclude `README.md` and any non-Markdown files.

Record:

```text
Context used:
07_podcast/source_briefs/[latest-or-only-filename].md
```

## Step 3 — Missing Context Response

If no user context exists and no source brief can be resolved, stop before
generating a script. Reply:

```text
Stage 2 context is missing.

I could not find a matching source brief in:

07_podcast/source_briefs/

Please provide one of the following:

1. NotebookLM recap
2. NotebookLM transcript
3. Source brief file path
4. Your own summary of the NotebookLM discussion
```

## Step 4 — Context Usage Boundary

Resolved context may be used only to:

1. connect the opening to the NotebookLM topic;
2. confirm that the user-provided Model Sentence remains on topic;
3. produce a natural teaching explanation;
4. make examples for the user-provided Vocabulary / Expressions relevant to the
   topic.

It must not be used to:

- choose or replace the Core Pattern;
- create or replace the Model Sentence;
- choose or add Vocabulary / Expressions;
- regenerate the NotebookLM discussion;
- perform new external research;
- update the Knowledge Base;
- update Stage 1 source briefs.

If the Model Sentence conflicts with the resolved context, flag the mismatch and
ask the user to revise it. Do not silently rewrite it.

## Step 5 — Completion Report

When the Stage 2 generator finishes an Output Drill Script, include one of:

```text
Context used:
User-provided NotebookLM Recap / Context
```

or:

```text
Context used:
07_podcast/source_briefs/[filename].md
```
