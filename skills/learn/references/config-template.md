# Config template

Copy the block below to `.claude/learn.config.md` in your project (or `~/.claude/learn.config.md`
for a default across projects) and edit it. Paths are relative to the project root. Every field
is optional; the defaults are shown.

The frontmatter holds settings; the body is free text about the learner, which /learn reads
to choose entry points, analogies and reasons.

```markdown
---
language: English                 # every reply, option label and note /learn writes
sources:
  notes: [notes/]                 # folders of notes to draw candidates from
  recent_days: 3                  # prefer notes from the last N days
  highlights: ""                  # optional "best of the day" file or glob, e.g. notes/*highlights*.md
  reading_list: []                # files listing links / feed digests; "- [x]" marks read
concepts:
  folder: concepts/               # one note per concept
  familiarity_field: familiarity  # frontmatter field, 0–4
  review_fields: [last_review, next_review]
  quiz_table_heading: "## Quiz log"   # table appended to on each check or quiz
  my_notes_heading: "## My notes"     # where the learner's own understanding goes
quiz:
  list_file: quiz-this-week.md    # concepts picked or taught this week
  day: Friday                     # weekly quiz day; "none" to turn off
  records_folder: ""              # optional folder for one file per quiz
  questions: 5
reading:
  wpm: 250                        # words per minute; CJK uses chars_per_min
  chars_per_min: 400
session:
  default_minutes: 30             # recommended option when asking today's time budget
backlog:
  file: learn-backlog.md          # unpicked candidates kept for later
  max_offers: 3                   # expire after being shown this many times without a pick
  max_age_days: 14                # expire news-driven rows older than this
learner:
  takeaway_style: "one question tied to my own work, answerable in a sentence or two"
---

## About me
Who you are, what you work on, what you already know well and where you are weak.
Example: "Product manager at a logistics company. Comfortable with spreadsheets and SQL,
new to machine learning. I learn best from a concrete case first, then the theory."

## How to teach me
Preferences: analogies from which field, how long a session should be, what to avoid.
Example: "Analogies from supply chains. Ten minutes max per concept. No acronyms without
spelling them out."

## Extra rules (optional)
Anything project-specific: e.g. "after a session, ask before committing", "new concepts follow
my vault's template at templates/concept.md".
```

## Field notes

- **language** — any natural language. Teaching, options and written notes all follow it.
  Technical terms may keep the original on first use.
- **sources.notes / highlights / reading_list** — /learn only reads these. It never scans
  the whole drive.
- **concepts.*** — if your concept notes use different field names (e.g. `level`, `mastery`),
  set them here. A 1–5 scale is fine if you say so in "Extra rules"; /learn maps it onto its
  0–4 rubric.
- **quiz.list_file** — created on first use with a `| Date | Concept | Why |` table. If the
  file already exists with other columns, /learn follows the existing columns.
- **session.default_minutes** — /learn always asks for today's budget first; this is the
  pre-selected answer.
- **backlog.*** — see `backlog.md`. Delete the file any time to start fresh.
- **learner.takeaway_style** — the shape of the take-home question at the end of a guided
  reading.
- **About me / How to teach me** — the single most useful part. The more concrete
  ("I run a small online shop", "I already use X daily but can't explain how it works"),
  the better the entry points.
