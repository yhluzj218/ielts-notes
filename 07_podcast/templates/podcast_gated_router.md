# Podcast Gated Router

## Formal Triggers

Run this router when the user enters any of:

- `生成 Podcast`
- `產生 Podcast`
- `generate podcast`
- `根據這些資料產生 NotebookLM source brief`
- `Generate NotebookLM source brief`
- `產生 Output Drill Script`
- `產生 Chant`
- `生成 Chant`
- `generate chant`

These triggers do not authorise generation of an ungated, complete Podcast. Inspect
the user input first and route exactly one stage.

## Case A — Stage 1: NotebookLM Source Brief

Run Stage 1 when the request contains:

```markdown
# NotebookLM Source Input
```

or when the user supplies an IELTS question, model essay, article, source notes,
existing viewpoints, or Research Mode for the purpose of creating a Podcast.

Controller:

`07_podcast/templates/source_brief_workflow.md`

Outputs:

- Source Log;
- NotebookLM Source Briefing Article;
- NotebookLM Generation Prompt.

Storage:

`07_podcast/source_briefs/`

Stage 1 must not generate an Output Drill, ElevenLabs/TTS script, Teacher Mode, or
Shadowing.

## Case B — Stage 2: ElevenLabs Output Drill Script

Run Stage 2 when the request contains:

```markdown
# Output Drill Input
```

or when the user enters `產生 Output Drill Script`.

Controller:

`07_podcast/templates/output_drill_workflow.md`

Stage 2 uses only the user-provided Topic, Core Pattern, Model Sentence, Vocabulary /
Expressions, optional Practice Topics, and context resolved by the Stage 2 gate.

Stage 2 must not regenerate the NotebookLM discussion, choose a pattern, choose
vocabulary, perform external research, or update the Knowledge Base.

## Case C — Stage 3: IELTS Chunk Memory Chant

Run Stage 3 when the request contains:

```markdown
# Chant Input
```

or a non-empty:

```text
Target sentence pattern:
...
```

Direct triggers `產生 Chant`, `生成 Chant`, and `generate chant` also route to Stage
3 and apply its required-input gate.

Controller:

`07_podcast/templates/chant_workflow.md`

Stage 3 generates one chant lyric package and one Suno prompt. It must not select
the Target Sentence Pattern, rerun Stage 1 or Stage 2, perform research, or update
the Knowledge Base.

## Ambiguous or Missing Input

If inputs for two or more stages are present, do not run them together. Ask the
user which single stage to run.

If a generic Podcast trigger contains neither recognisable Stage 1 material nor an
Output Drill or Chant input, stop and reply:

```text
Podcast input is missing.

Please provide either:

1. # NotebookLM Source Input
   for a Source Briefing Article and NotebookLM Generation Prompt

or

2. # Output Drill Input
   for an ElevenLabs Output Drill Script

or

3. # Chant Input
   for an IELTS Chunk Memory Chant and Suno Prompt
```
