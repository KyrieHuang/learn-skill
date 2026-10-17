# Candidate backlog

Material does not arrive evenly. One day has ten good picks, the next has one. The backlog keeps
good candidates the user did not pick so they can come back, and so a thin day is filled from
earlier ones instead of being padded.

## File

`backlog.file` in the config (default `learn-backlog.md`). Create it with this header if missing:

```markdown
| Added | Category | Candidate | Source | Reason | Minutes | Offered | Last offered | Status |
|---|---|---|---|---|---|---|---|---|
```

- **Category**: `question` / `concept` / `read`
- **Source**: wikilink or path of the note it came from (concepts: the concept note)
- **Offered**: how many times it has been shown
- **Status**: `open` / `picked` / `done` / `dropped` / `expired`

Follow the existing columns if the file already has a different header.

## After every candidate round

- Every candidate shown and **not picked** → add a row (`Offered 1`) or, if it is already in the
  backlog, increase `Offered` and set `Last offered` to today.
- Picked → `picked`; set `done` when the item is finished.
- Picked but not done (trimmed by the time budget, or the session ended) → stays `picked` and is
  offered again first next time, labelled "picked last time, not done yet". It does not count
  toward `max_offers`: the user already said yes once.
- The user choosing "never show this again" → `dropped`.

## When building candidates

1. Build today's candidates as usual (SKILL.md §2).
2. Pull `picked` (not done) and `open` backlog rows of the same category and rank them **together with today's**, by the
   same signals. Old rows are not second-class: a strong pick from three days ago beats a weak
   one from today.
3. Mark backlog picks in the option description: "From 10-15 · offered once before".
4. Still five at most per category, and still never pad: if today plus the backlog give two good
   picks, show two.

## Staleness

- A row offered `backlog.max_offers` times (default 3) without being picked → `expired`. Showing
  the same thing a fourth time is noise; the user has answered.
- A row older than `backlog.max_age_days` (default 14) → `expired`, unless its source is
  evergreen (a concept note, a long-form article rather than a news item).
- News-driven questions age fast: prefer today's version of the same theme over an older one,
  and expire the older one when a newer question covers it.
- Concepts never really expire from the map; an expired concept row only stops being *pushed*.
  The concept note keeps its familiarity and can come back when new material uses it again
  (then add a fresh row).

## Telling the user

At the top of the first candidate box, one line: "Today: 7 new + 3 from the backlog
(4 still open)." So the user knows nothing good is lost by not picking it today.
