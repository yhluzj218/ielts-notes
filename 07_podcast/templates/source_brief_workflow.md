# Generate NotebookLM Source Brief — Workflow

## Triggers

Run this workflow directly when the user says:

- `根據這些資料產生 NotebookLM source brief`
- `Generate NotebookLM source brief`

Also run it when `podcast_gated_router.md` selects Stage 1 from a formal generic
Podcast trigger plus Stage 1 material.

The request must include or point to user-selected source material. The old
night-before commands `幫我產生明天的 Podcast`, `generate tomorrow podcast`, and
`幫我準備明天的 Podcast` remain disabled.

## Scope

The workflow produces only this Phase 1 package:

1. a Source Log in Research-Assisted Mode;
2. a NotebookLM Source Briefing Article;
3. a NotebookLM Generation Prompt.

Do not generate a full Podcast, host transcript, audio script, ElevenLabs/TTS text,
Teacher Mode, Shadowing, Interactive Output, output drill, chant, or music prompt.

## Step 1 — Validate the Input

Accept the structure in [`source_input_template.md`](source_input_template.md), but
also accept unstructured user material when the same information is clear.

The user must provide at least one substantive source:

1. IELTS question;
2. model essay;
3. article;
4. source notes;
5. NotebookLM notes;
6. user's own viewpoints.

Validation rules:

- A topic name alone is not a substantive source.
- Do not choose a topic for the user.
- A neutral topic label may be derived from an unambiguous supplied IELTS question
  or source; this is labelling, not topic selection.
- The material must identify a topic or issue clearly enough to brief it.
- In Strict Source Mode, the user material must support at least three
  distinguishable viewpoints.
- In Research-Assisted Mode, validate the three-viewpoint requirement after
  research against the combined user material and reliable external sources.
- A viewpoint may be an advantage, disadvantage, cause, solution, opinion, or
  qualified position, but its reasoning must be traceable to an allowed source.
- An IELTS question alone may seed Research-Assisted Mode. In Strict Source Mode it
  is sufficient only when its wording supports the required viewpoints without
  inventing reasons, examples, or factual claims.
- If a Desired Position is supplied, the final allowed source set must contain
  enough support for that position. Do not manufacture support to satisfy the
  preference.

If the initial source requirement or the final evidence requirement fails, reply
with:

```text
Source is insufficient.

Please provide at least one of the following:
1. IELTS question
2. model essay
3. article
4. source notes
5. your own viewpoints
6. permission to use Research-Assisted Mode with external sources
```

Then list exactly what is missing and ask the user to provide it. Do not create a
brief file.

## Step 2 — Resolve the Research Mode

### Mode A — Strict Source Mode

Use this mode when the user explicitly selects `Strict Source Mode`.

Allowed:

- reorganise;
- paraphrase;
- classify;
- simplify;
- compare;
- combine overlapping ideas from the supplied material;
- derive a cautious conclusion from the supplied arguments.

Not allowed:

- external knowledge presented as support;
- invented facts, statistics, studies, dates, named examples, quotations, or
  historical claims;
- a concrete example that is not present in the source;
- silently filling evidence gaps.

For `Example or support`, use only supplied evidence. If a viewpoint is otherwise
well supported but has no example, write `No example was supplied in the source
material.` If missing support makes the viewpoint too thin, return
the full `Source is insufficient.` response instead.

### Mode B — Research-Assisted Mode

This is the default for the current Phase 1 workflow. The input template explicitly
sets `Research-Assisted Mode`. If the user explicitly selects `Strict Source Mode`,
Mode A overrides this default.

The user's material remains the primary source. External research may add context,
contrast, examples, or additional viewpoints, but it may not silently override the
user's material. If an external source conflicts with the supplied material, label
the conflict and present both claims; do not resolve it without evidence.

Research rules:

1. Prefer official reports from organisations such as the UN, UNEP, OECD, World
   Bank, WHO, government statistics offices, and official policy bodies.
2. Next prefer peer-reviewed journals, university research, and established
   research institutes.
3. Reputable educational or media sources such as BBC, Reuters, AP, Financial
   Times, The Economist, The Guardian, The Conversation, and National Geographic
   may provide accessible context.
4. Topic-specific professional organisations may be used when their expertise,
   authorship, and publication details are clear.
5. Avoid personal blogs, SEO content farms, unknown websites, unverifiable social
   posts, pages without authorship/publication information, and unsourced figures.
   If a weaker source is indispensable for representing a claim, label it as weak
   in the Reliability note and do not use it as the sole support for a factual
   conclusion.
6. Every external factual claim, figure, concrete example, or study finding must be
   supported by a cited source.
7. Do not use a figure merely because it appears in a search-result snippet.
8. Label unresolved uncertainty explicitly as `[Uncertain: ...]`.
9. Produce the Source Log before the briefing article.

Source Log format:

```markdown
## Source Log

### Source 1

Title:
...

Publisher / Organisation:
...

Source type:
Official report / Academic article / Reputable news / Educational source / Other

Link:
...

Key idea used:
...

Which part of the brief it supports:
Background / Viewpoint 1 / Viewpoint 2 / Viewpoint 3 / Weighing the Arguments / Final Position

Reliability note:
Explain why this source is credible and note any relevant limitation.
```

If reliable external sources are insufficient but the user's material can still
support a limited brief, include:

```text
Research note:
Reliable sources were insufficient for this topic. The brief below is based mainly on user-provided material.
```

If neither external research nor the user's material is sufficient, do not create a
file. Return the full `Source is insufficient.` response from Step 1.

Evidence may support background, viewpoints, examples, common disputes, solutions,
or comparison of advantages and disadvantages. Keep evidence concise and translate
it into useful IELTS reasoning; do not turn the brief into a research report.

When using a number, state its source clearly. Prefer a plain-language causal idea
over a statistic when the number is not essential.

## Step 3 — Determine the Question Type

If the user supplies a Question Type, verify it against the question. If it
conflicts with the wording, explain the mismatch and use the type supported by the
question.

If the field is blank, classify only from the supplied IELTS Question:

- Opinion
- Agree / Disagree
- Discuss both views
- Advantages / Disadvantages
- Advantages / Disadvantages + Opinion
- Problem / Solution
- Cause / Solution
- Two-part question

If no IELTS Question is supplied, write:
`Not determinable — IELTS Question not supplied.`

After the classification, add one short explanation:
`This is a [question type] question because...`

Question-type classification does not authorise adding ideas or facts.

## Step 4 — Generate the Phase 1 Outputs

Use [`source_brief_template.md`](source_brief_template.md) exactly.

Content rules:

- Use clear, natural English.
- Keep Background concise and source-bound.
- When Background uses external information, name the supporting organisation
  briefly in the text.
- Build three viewpoints; add Viewpoint 4 only when the source clearly supports it.
- Keep each viewpoint distinct rather than splitting one argument into several
  paraphrases.
- Label every viewpoint's Source basis as `User-provided material`, `External
  source`, or `Both`.
- Include one Natural IELTS sentence for each viewpoint.
- Include `Possible Solutions or Responses` only when the question requires a
  solution or the supplied topic naturally supports responses. For each response,
  explain what it is, why it helps, and one limitation.
- `Weighing the Arguments` must compare the strength, relevance, and limitations of
  the supplied support. Do not create new evidence.
- Use the user's Desired Position when it is supported. Otherwise state the source
  limitation or use a cautious position.
- Useful Vocabulary and Expressions must come from the supplied source or from
  neutral paraphrases used in the brief. Language items must not smuggle in new
  factual claims.
- The NotebookLM Generation Prompt must prohibit facts beyond the source.

## Step 5 — Save and Report

Save successful output to:

`07_podcast/source_briefs/YYYY-MM-DD_notebooklm_source_brief_<topic-slug>.md`

Use the current local date. Derive the slug only from the user-supplied topic or the
clearly identified topic in the supplied material. If the name exists, add `-02`,
then increment as needed.

Do not update:

- `10_knowledge_base/`;
- `09_coach/knowledge_review_queue.md`;
- performance or error databases;
- Sprint or Theme Sprint progress;
- legacy `07_podcast/episodes/`.

Report:

1. mode used;
2. topic and question type;
3. supplied source types used;
4. saved path;
5. Source Log status;
6. any uncertainty or omitted material.
