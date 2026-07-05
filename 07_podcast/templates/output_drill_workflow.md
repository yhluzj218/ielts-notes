# Stage 2 — ElevenLabs Output Drill Workflow

## Purpose

Generate one ElevenLabs-ready Output Drill Script from user-selected language
material and resolved Stage 1/NotebookLM context.

Do not regenerate a NotebookLM discussion. Do not perform external research. Do not
update the Knowledge Base.

## Required Input

Use [`output_drill_input_template.md`](output_drill_input_template.md):

```markdown
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

Required:

- Topic;
- Core Pattern;
- Model Sentence;
- three to five Vocabulary / Expressions.

Optional:

- Practice Topics;
- NotebookLM Recap / Context;
- Source Brief File.

Practice Topics may be blank. If none are supplied, keep Interactive Output on the
main Topic; do not invent replacement topics.

## Step 1 — Gate Check

Apply [`stage2_context_gate.md`](stage2_context_gate.md).

If Topic, Core Pattern, Model Sentence, or the minimum three Vocabulary /
Expressions are missing—or more than five Vocabulary / Expressions are supplied—
stop and return the gate's `Output drill input is incomplete.` response.

Never infer, select, replace, or silently rewrite the Core Pattern, Model Sentence,
or Vocabulary / Expressions.

## Step 2 — Resolve Context

Use the exact priority order in
[`stage2_context_gate.md`](stage2_context_gate.md):

1. User-provided NotebookLM Recap / Context
2. Explicit Source Brief File
3. Unique Topic match in `07_podcast/source_briefs/`
4. Only source brief, or latest when the user explicitly says `用最新的`

If multiple files are plausible, ask the user to choose. If no context can be
resolved, return `Stage 2 context is missing.` and stop.

The resolved context may guide topic continuity and examples, but it is not a source
of new target language.

## Step 3 — Validate Alignment

Before generation:

1. Check whether the Model Sentence is a valid use of the Core Pattern.
2. Check whether the Model Sentence is relevant to the Topic and resolved context.
3. Check whether all Vocabulary / Expressions can be used naturally.

If there is a material mismatch, identify it and ask the user to revise the input.
Do not repair required input silently.

## Step 4 — Generate the ElevenLabs-ready Script

Do not include `[TEACHER]` or any other speaker label. The script must begin
directly with the spoken text.

Use only pause durations that are multiples of three seconds. The standard pause
markers are:

```text
[pause 3 seconds]
[pause 6 seconds]
[pause 9 seconds]
[pause 12 seconds]
```

The script must contain these sections in order:

### 1. Opening Transition

- Begin with a warm, upbeat welcome such as `Welcome!` or `Welcome back!`.
- Connect briefly to the resolved NotebookLM/source-brief topic.
- State that the goal is to turn the discussion into spoken output.
- Sound cheerful and inviting while keeping the language natural and concise.
- Do not summarise or recreate the full NotebookLM discussion.

### 2. Pattern Teaching

- Record the user-provided Core Pattern exactly in the Markdown metadata, but do not
  read abstract bracket labels aloud when they would be hard to understand.
- Begin the spoken teaching with the complete user-provided Model Sentence.
- Explain the sentence in short, conversational English: first say what the opening
  part does, then say what the ending adds.
- Prefer listening-friendly phrases such as `This sentence does two things`,
  `First, it accepts the benefit`, and `Then, it adds the problem`.
- Explain only one necessary grammar or word-choice point at a time, using the
  actual words in the Model Sentence.
- Avoid technical labels such as `auxiliary verb`, `base form`, `subordinate
  clause`, or `concessive clause` unless the user explicitly asks for grammar
  terminology.
- Keep individual explanation sentences short enough to understand by listening.
- Do not introduce a second pattern.

### 3. Vocabulary Focus

For each of the three to five user-provided Vocabulary / Expressions:

- give a concise plain-English meaning;
- give one topic-relevant example grounded in the resolved context;
- leave a short pause for repetition.

Do not add extra vocabulary targets. Examples must not introduce unsupported factual
claims; use source-grounded or clearly hypothetical wording.

### 4. Shadowing

- Practise the user-provided Model Sentence.
- First model the complete sentence.
- Break it into only the natural chunks needed for pronunciation.
- End with at least one complete-sentence repetition.
- Do not replace the Model Sentence with a rewritten version.

### 5. Interactive Output

- If Practice Topics were supplied, use only those topics.
- If Practice Topics are blank, remain on the main Topic.
- Ask the learner to produce a sentence using the Core Pattern and, where natural,
  one user-provided Vocabulary / Expression.
- Give `[pause 12 seconds]` before any sample answer.
- Keep sample answers consistent with the resolved context and target language.

### 6. Final Turn

- Ask for one independent final sentence using the Core Pattern.
- Encourage use of one user-provided Vocabulary / Expression where natural.
- Leave `[pause 12 seconds]`.
- Thank the learner for listening or practising.
- End with a warm transition to the next song or `today's chant`.
- Do not introduce new teaching content.

## Step 5 — File Format and Storage

Save to:

`07_podcast/output_drills/YYYY-MM-DD_output_drill_<topic-slug>.md`

Use the current local date and a slug derived only from the user-provided Topic. If
the path already exists, append `-02`, `-03`, and so on.

File structure:

```markdown
# Output Drill Script — [Topic]

Context used:
[User-provided NotebookLM Recap / Context or repo-relative source brief path]

Core Pattern:
[Exact user-provided Core Pattern]

## ElevenLabs-ready Script

...
```

Only the content under `## ElevenLabs-ready Script` is intended to be pasted into
ElevenLabs.

## Step 6 — Completion Report

Report:

- saved file path;
- Topic;
- Core Pattern;
- number of Vocabulary / Expressions used;
- whether Practice Topics were supplied;
- context source.

Always include:

```text
Context used:
User-provided NotebookLM Recap / Context
```

or:

```text
Context used:
07_podcast/source_briefs/[filename].md
```

## Restrictions

- Do not choose or replace the Core Pattern.
- Do not create or replace the Model Sentence.
- Do not choose or add Vocabulary / Expressions.
- Do not regenerate the NotebookLM discussion.
- Do not generate a Stage 3 chant as a side effect.
- Do not perform external research.
- Do not update the Knowledge Base, Stage 1 brief, Sprint, or performance/error DB.
