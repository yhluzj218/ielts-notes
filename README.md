# IELTS Coach

Personal IELTS study notes + the source of an AI-powered IELTS Coach application.

The notes folders (`00_dashboard` → `08_ai`) are the living knowledge base that feeds the coach. The `09_coach` folder is where the product gets built.

---

## Folder Tree

```
ielts-notes/
├── 00_dashboard/               # Goals, study plan, weekly reviews, progress tracking
├── 01_lessons/                 # Lesson notes by teacher and skill
│   ├── speaking/               # Joe's speaking lessons
│   ├── writing/                # Matt's writing lessons
│   ├── index.md
│   └── teacher.md              # Principles distilled from both teachers
├── 02_writing/                 # Writing practice
│   ├── task1/
│   │   ├── drafts/
│   │   ├── feedback/
│   │   └── models/
│   ├── task2/
│   │   ├── drafts/
│   │   ├── feedback/
│   │   └── models/
│   ├── models_index.md
│   └── writing_notes.md
├── 03_speaking/                # Speaking practice
│   ├── part1/ part2/ part3/
│   ├── practice/
│   │   ├── chat/
│   │   └── situation/
│   └── speaking_notes.md
├── 04_listening/               # Listening mistakes and strategies
├── 05_reading/                 # Reading mistakes and strategies
├── 06_error_database/          # Categorised error log
│   ├── error_log.md            # Master log (auto-appended after each lesson)
│   ├── grammar/
│   ├── listening/
│   ├── speaking/
│   ├── vocabulary/
│   └── writing/
├── 07_podcast/                 # Commute shadowing plan
├── 08_ai/                      # AI layer: prompts, rubrics, templates, Anki
│   ├── prompts/                # Active coach prompts
│   │   └── coach_prompt.md
│   ├── teachers/               # Per-teacher style profiles for AI grading
│   ├── templates/              # Output templates (feedback, model essays, Anki)
│   ├── rubrics/                # Scoring rubrics (IELTS official + teacher calibration)
│   ├── workflows/              # Multi-step automation specs
│   └── anki/                   # Generated Anki card files
│       ├── writing/
│       └── speaking/
└── 09_coach/                   # AI Coach application (MVP)
    └── README.md
```

---

## Key Files

| Purpose | File |
|---|---|
| AI coach instructions | [08_ai/prompts/coach_prompt.md](08_ai/prompts/coach_prompt.md) |
| Teacher principles | [01_lessons/teacher.md](01_lessons/teacher.md) |
| Error log | [06_error_database/error_log.md](06_error_database/error_log.md) |
| Writing notes | [02_writing/writing_notes.md](02_writing/writing_notes.md) |
| Speaking notes | [03_speaking/speaking_notes.md](03_speaking/speaking_notes.md) |
| Product requirements | [PRD.md](PRD.md) |
| Architecture decisions | [DECISIONS.md](DECISIONS.md) |
| Coach app | [09_coach/](09_coach/) |

---

## Docs

- [PRD.md](PRD.md) — product vision and MVP scope
- [DECISIONS.md](DECISIONS.md) — architecture decision log
- [CLAUDE.md](CLAUDE.md) — instructions for the Claude Code AI coach
