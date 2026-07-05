# 07_podcast/ — Podcast Workflow

The active workflow currently has:

1. **Stage 1 — Generate NotebookLM Source Brief**
2. **Stage 2 — Generate ElevenLabs Output Drill Script**
3. **Stage 3 — Generate IELTS Chunk Memory Chant + Suno Prompt**

Both stages are controlled by
[`templates/podcast_gated_router.md`](templates/podcast_gated_router.md). The router
does not directly make an ungated, complete Podcast.

## Formal Triggers

- `生成 Podcast`
- `產生 Podcast`
- `generate podcast`
- `根據這些資料產生 NotebookLM source brief`
- `Generate NotebookLM source brief`
- `產生 Output Drill Script`
- `產生 Chant`
- `生成 Chant`
- `generate chant`

The router inspects the supplied input before selecting one stage.

## Stage 1

Use either command after providing source material:

```text
根據這些資料產生 NotebookLM source brief
```

```text
Generate NotebookLM source brief
```

## Required Input

The user must provide at least one of:

- an IELTS question;
- a model essay;
- an article;
- source notes;
- NotebookLM notes;
- the user's own viewpoints.

A topic label by itself is not source material. If the supplied material and
permitted research cannot support a grounded briefing article with at least three
viewpoints, the workflow returns `Source is insufficient.` and asks for the missing
material. It does not create a file.

Copy the supported input format from
[`templates/source_input_template.md`](templates/source_input_template.md).

## Modes

### Strict Source Mode

The brief may reorganise, paraphrase, classify, simplify, and compare only the
material supplied by the user. It must not add external facts, statistics, examples,
or unsupported factual claims.

### Research-Assisted Mode — current default

The input template currently selects this mode. External research must come from
credible sources and must be documented in a Source Log before the briefing
article. User material remains the primary source; unsupported facts remain
prohibited, conflicts must be labelled, and uncertainty must be marked.

## Output

One Markdown file contains:

1. `Source Log` — Research-Assisted Mode only;
2. `NotebookLM Source Briefing Article`;
3. `NotebookLM Generation Prompt`.

The fixed format and validation rules are defined in:

- [`templates/source_brief_workflow.md`](templates/source_brief_workflow.md)
- [`templates/source_brief_template.md`](templates/source_brief_template.md)

## Stage 2

When the user asks for a Stage 2 Output Drill and supplies
`# Output Drill Input`, validate it with:

- [`templates/output_drill_input_template.md`](templates/output_drill_input_template.md)
- [`templates/stage2_context_gate.md`](templates/stage2_context_gate.md)
- [`templates/output_drill_workflow.md`](templates/output_drill_workflow.md)

Stage 2 requires the user to provide Topic, Core Pattern, Model Sentence, at least
three and no more than five Vocabulary / Expressions. Practice Topics, NotebookLM
Recap / Context, and Source Brief File are optional.

Context is resolved in this order:

1. user-provided NotebookLM Recap / Context;
2. explicit Source Brief File;
3. a unique topic match in `source_briefs/`;
4. the only source brief, or the latest source brief when the user explicitly asks
   for it.

If multiple source briefs are plausible, the system lists them and asks the user to
choose. Source briefs supply context only; they never supply the Core Pattern, Model
Sentence, or Vocabulary / Expressions.

After the gate passes, Stage 2 generates:

1. Opening Transition
2. Pattern Teaching
3. Vocabulary Focus
4. Shadowing
5. Interactive Output
6. Final Turn

It begins directly with spoken text, without `[TEACHER]` or other speaker labels.
The opening gives a warm, upbeat welcome, and the ending thanks the listener before
transitioning to the next song or today's chant. Pause markers use only multiples
of three seconds. The script is saved to:

`07_podcast/output_drills/YYYY-MM-DD_output_drill_<topic-slug>.md`

Pattern Teaching begins with the complete Model Sentence and explains it in short,
conversational English. The bracket template is retained in metadata but is not read
aloud when it would be difficult to understand by listening.

## Stage 3

When the request includes `# Chant Input` or `Target sentence pattern:`, run:

- [`templates/chant_input_template.md`](templates/chant_input_template.md)
- [`templates/chant_workflow.md`](templates/chant_workflow.md)

The Target Sentence Pattern is required and must be supplied by the user.
Substitution Ideas, IELTS Topic Links, and Music Style are optional.

Stage 3 generates one 1–1.5 minute repetitive speaking-drill chant, a substitution
bank, topic links, and one Suno prompt. The default style is a simple nursery-rhyme
chant; light bossa nova is optional.

Storage:

`07_podcast/chants/YYYY-MM-DD_chant_<pattern-slug>.md`

## Storage

Successful briefs are stored as:

```text
07_podcast/source_briefs/YYYY-MM-DD_notebooklm_source_brief_<topic-slug>.md
```

If a file with the same date and slug already exists, append `-02`, `-03`, and so
on. A `Source is insufficient.` response creates no file.

## Legacy Material

`episodes/`, `characters/`, `world/`, `songs/`, and `commute_plan.md` are historical
materials from earlier Podcast systems. They are not read or updated by the active
Phase 1 workflow.
