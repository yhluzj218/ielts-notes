# Ideas — Reusable IELTS Argument Bank

> Single Source of Truth for IELTS reusable ideas.
> Last updated: 2026-07-04

---

## What this is

This folder is the **one place** where reusable IELTS ideas (arguments, angles, causal
logic) live. It exists so Writing, Speaking, Podcast, and Sprint planning all draw on
the *same* pool of ideas instead of each keeping their own separate copy.

- **Writing** (`02_writing/`) links to ideas here instead of re-explaining the argument.
- **Speaking** (`03_speaking/`) links to the same ideas for Part 2 / Part 3 answers.
- **Podcast** (`07_podcast/`) links to the same ideas when building an episode's Speaking segment.
- **Theme Sprint** (`09_coach/sprints/THEME_SPRINT_TEMPLATE.md`) links to a theme folder here as its "Source Ideas" — it does not copy idea content into the sprint file.

## What this is NOT

- Not a place for full essays. Full drafts live in `02_writing/task1/` or `02_writing/task2/`.
- Not a place for full spoken answers. Full Speaking answers live in `03_speaking/`.
- Not a place for Podcast Episode Packages. NotebookLM source/prompts and ElevenLabs
  shadowing scripts live in `07_podcast/episodes/season_01/`.
- Not a vocabulary list. Reusable expressions live in `10_knowledge_base/expressions/`.

One file here = one reusable idea, atomic, theme-tagged, linkable.

---

## Folder structure

```
10_knowledge_base/ideas/
  INDEX.md              ← this file
  TEMPLATE.md            ← copy this to create a new idea note
  MIGRATION_PLAN.md      ← plan for pulling ideas out of existing long files
  education/
  technology-ai/
  environment/
  health/
  work-career/
  family-children/
  government-society/
  culture-tourism/
```

Each theme folder holds atomic idea notes named after the claim itself, e.g.
`online-learning-increases-accessibility.md`.

---

## Idea Index by Theme

### Education
- *(none yet)*

### Technology & AI
- [Access to goods and services has become democratised](technology-ai/access-to-goods-and-services-has-become-democratised.md)

### Environment
- [Small individual actions cause large collective harm](environment/small-individual-actions-cause-large-collective-harm.md)

### Health
- *(none yet)*

### Work & Career
- [Job creation does not guarantee job quality](work-career/job-creation-does-not-guarantee-job-quality.md)

### Family & Children
- *(none yet)*

### Government & Society
- [No long-term stake leads to irresponsible behaviour](government-society/no-long-term-stake-leads-to-irresponsible-behaviour.md)

### Culture & Tourism
- [Commercialisation erodes cultural authenticity](culture-tourism/commercialisation-erodes-cultural-authenticity.md)
- [Profit leakage limits local economic benefit](culture-tourism/profit-leakage-limits-local-economic-benefit.md)

---

## Migration status

The former `10_knowledge_base/writing/ideas.md` (6 reusable ideas) has been fully migrated
into the atomic notes above and the original file has been removed. See
`MIGRATION_PLAN.md` for the full record of what moved where. `10_knowledge_base/ideas/` is now
the only place Reusable Ideas are stored — see `10_knowledge_base/ARCHITECTURE.md` for the
overall design.
