# Stage 3 — IELTS Chunk Memory Chant Workflow

## Purpose

Generate one short speaking-drill chant and one Suno-ready music prompt from a
user-provided IELTS sentence pattern.

The chant is a memory and pronunciation tool, not a full IELTS answer and not a
normal pop song.

## Trigger

Run Stage 3 when the Podcast router receives:

- `# Chant Input`;
- `Target sentence pattern:` plus a pattern;
- `產生 Chant`;
- `生成 Chant`;
- `generate chant`.

The generic `生成 Podcast` / `產生 Podcast` / `generate podcast` triggers may route
to Stage 3 only when Chant Input or a Target Sentence Pattern is present.

## Required Input

The user must provide exactly one:

```markdown
## Target Sentence Pattern
...
```

or:

```text
Target sentence pattern:
"..."
```

Do not select or extract a Target Sentence Pattern automatically from Stage 1,
Stage 2, the Knowledge Base, or a previous conversation.

If it is missing, stop and reply:

```text
Chant input is incomplete.

Please provide:

# Chant Input

## Target Sentence Pattern
...

## Substitution Ideas
1.
2.
3.
4.
5.
```

## Optional Input

- Substitution Ideas
- IELTS Topic Links
- Music Style

If Substitution Ideas are supplied, preserve them when natural. Generate additional
simple substitutions only as needed to produce a total bank of five to eight.

If IELTS Topic Links are blank, infer up to four broad IELTS topics from the pattern
and substitutions. Do not add factual claims.

Music Style options:

- `Nursery-rhyme chant` — default
- `Light bossa nova chant`

## Lyrics Rules

Generate one chant with:

- an approximate performance length of 1–1.5 minutes;
- very simple English;
- very short lines;
- strong, steady repetition;
- a clear chorus;
- simple rhyme where natural;
- the exact Target Sentence Pattern repeated many times;
- five to eight natural substitutions;
- IELTS Speaking Part 1, Part 2, or Part 3 relevance;
- a simple child-friendly chant or nursery-rhyme feel;
- flexible sentence endings that work as a speaking drill.

Do not:

- write poetic or abstract lyrics;
- use difficult vocabulary;
- write a full IELTS answer;
- imitate a real artist, singer, or copyrighted song;
- introduce a second target pattern;
- distort the target pattern merely to force a rhyme.

Make the chorus highly repetitive: simple, rhythmic, slightly silly when helpful,
but still useful for IELTS Speaking.

## Lyrics Output Format

```markdown
Title:
[Simple song title]

Lyrics:

[Verse 1]
...

[Chorus]
...

[Verse 2]
...

[Chorus]
...

[Ending]
...

Pattern practised:
[Target pattern]

Substitution bank:
- [substitution 1]
- [substitution 2]
- [substitution 3]
- [substitution 4]
- [substitution 5]
- [substitution 6 if useful]
- [substitution 7 if useful]
- [substitution 8 if useful]

IELTS topic links:
- [topic 1]
- [topic 2]
- [topic 3]
- [topic 4]
```

## Suno Prompt Rules

Every prompt must begin with:

```text
Use my saved voice profile.
```

Shared requirements:

- natural female lead vocal;
- mostly spoken-singing with a simple melody;
- short lines with clear pauses for shadowing;
- extremely clear pronunciation;
- clearly articulated consonants and word endings;
- lead vocal louder and clearer than backing vocals;
- simple call-and-response;
- light background harmonies only in the chorus;
- strong repetition of the Target Sentence Pattern;
- clarity, repetition, and intelligibility over musical complexity;
- no dramatic singing, strong vibrato, belting, complex runs, mumbling, breathy
  delivery, electronic dance beat, or cartoon voice;
- do not imitate any real singer or artist.

### Nursery-rhyme chant — default

Specify:

- simple and cheerful English children's learning-song feel;
- slow-to-medium tempo, not fast;
- light acoustic guitar, gentle hand claps, soft shaker, and simple percussion;
- a very simple melody and strong steady rhythm;
- enough space after every phrase for comfortable repetition.

### Light bossa nova chant

Specify:

- light, upbeat, warm bossa nova groove;
- medium tempo, not too slow;
- warm nylon-string acoustic guitar;
- light shaker, soft percussion, and walking bass;
- relaxed, sunny, memorable mood;
- no jazz improvisation and no dense arrangement.

Generate only the prompt for the selected Music Style.

## File Format and Storage

Save to:

`07_podcast/chants/YYYY-MM-DD_chant_<pattern-slug>.md`

Use the current local date. Build the slug from the shortest recognisable fixed
words in the user-provided pattern. If the path exists, append `-02`, `-03`, and so
on.

File structure:

```markdown
# Chant Package — [Title]

## Lyrics

[Lyrics Output Format]

## Suno Prompt

[Ready-to-paste prompt]
```

## Completion Report

Report:

- saved file path;
- Target Sentence Pattern;
- number of substitutions;
- IELTS topic links;
- selected Music Style.

## Restrictions

- Do not run Stage 1 or Stage 2 as a side effect.
- Do not choose the Target Sentence Pattern.
- Do not perform external research.
- Do not update the Knowledge Base, source briefs, output drills, Sprint, or
  performance/error DB.
