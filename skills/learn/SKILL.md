---
name: learn
description: >-
  Daily study companion. Reads the user's own notes and reading list, offers three kinds of
  candidates — a question worth thinking about, a foundational concept worth filling in, an
  article worth reading — five honest picks each with a reason and a time estimate, lets the
  user choose by clicking (multi-select), then works through the chosen items one at a time:
  a Socratic discussion for questions, a short lesson with check questions for concepts, a
  timed section-by-section guided reading for articles. Records familiarity (0–4), keeps a
  "this week's quiz" list and runs a weekly quiz on a fixed day. Use it when the user says
  /learn, "what should I learn today", "pick something for me to study", "teach me X",
  "walk me through this article", "quiz me", "今天學什麼", "陪我讀這篇", "教我 X", "出題考我",
  or when another workflow ends with "hand the daily three to /learn".
---

# /learn

Turn "I have a pile of notes and links" into twenty focused minutes of actually understanding
something. The user decides **what** to learn; Claude decides **how to teach it** and keeps an
honest record of what stuck.

Three rules hold everywhere:

1. **The user chooses.** Never pick "the one thing" for them. Offer real candidates and let them
   multi-select.
2. **Every candidate and every next step carries a time estimate** in minutes.
3. **Click, don't type.** Whenever the user has to choose or confirm, use a clickable choice box.
   Typing is only for open questions where their own words are the point (their opinion, their
   explanation).

How to drive the choice UI — option limits, why text before a choice box gets hidden, how to
fall back on clients without one — is in `references/claude-code-ui.md`. **Read it before the
first choice box of the session.**

## 0. Load the config

Look for the config in this order and use the first one found:

1. `.claude/learn.config.md` in the current project
2. `learn.config.md` in the project root
3. `~/.claude/learn.config.md` (a personal default for every project)

The config sets language, where the material lives, where concept notes live and how
familiarity is stored, the quiz list file, the quiz day, and who the learner is. Field
reference: `references/config-template.md`.

**No config?** Run a short setup: ask (with choice boxes, one batch) for language, the notes
folder, and the quiz day; offer "use defaults" for the rest; write `.claude/learn.config.md`
from the template; tell the user which file to edit later. Then continue — do not make setup a
separate session.

Reply in the configured `language` for everything the user sees, including option labels.

## 1. Gather material

Read only what the config points at:

- `sources.notes` — note folders. Prefer files from the last `sources.recent_days` days (by date
  in the filename, else modification time).
- `sources.reading_list` — files of links or feed digests. An item already marked read (`[x]`,
  `read: true`) is skipped.
- `sources.highlights` — an optional "best of the day" file. Good questions usually come from here.
- `concepts.folder` — concept notes with familiarity, to find weak foundations.

Do not fetch URLs yet; titles, summaries and the notes' own text are enough to pick candidates.
If the material is thin (fewer than 5 good candidates in a category), list fewer. **Never pad.**

If another workflow invoked /learn with today's material already in context (for example a
daily digest that just finished), use that and skip re-reading.

## 2. Build three candidate lists

Five per category, each a pick Claude would genuinely recommend:

| Category | Draw from | Each candidate states |
|---|---|---|
| ① A question worth thinking about | highlights, notes with tension or disagreement | the question in one line · why it is worth the user's time · minutes |
| ② A foundational concept to fill in | concept notes with low familiarity that today's material leans on; foundations before branches | the concept · which of today's items it unlocks · minutes |
| ③ Something worth reading in full | long-form pieces in notes or the reading list | title · why this one · reading minutes |

Ranking signals, in order: connects to something the learner already works on (`learner`
section of the config) → unlocks several of today's items at once → fills a low-familiarity
foundation → novelty. Use the learner's background to phrase reasons ("this is why your
long sessions get expensive"), not generic ones.

Time estimates: question 10–20 min; concept 10–15 min per familiarity level gained; article =
words ÷ the learner's reading speed (default 250 wpm, 400 characters per minute for CJK) plus
five minutes of discussion. Round to 5.

## 3. Let the user choose

Follow `references/claude-code-ui.md`: multi-select, five candidates split 3 + 2, reason and
minutes in each option's description, and nothing the user needs to read placed before the
box. Two rounds: ① and ② in the first box (four questions: ①a ①b ②a ②b), ③ plus anything
else to confirm in the second.

Then one more box: **which one first?** List the picked items with their minutes; recommend
an order (usually concept → article → question, because the concept makes the other two
easier) and mark the recommendation.

Write every picked concept into the quiz list now (§6), so it is recorded even if the session
ends early.

## 4. Work through items — one at a time

Start each item by saying how long it should take. Finish it before opening the next one; at
the end of each item, offer "next item / take a break / stop here" as a choice.

All teaching content goes **inside the choice box's question field**, with choices such as
"done, ask me" / "explain it another way" / "go deeper" — see the UI reference for why.

| Picked | Mode | Reference |
|---|---|---|
| ① question | Discussion: ask their view first, follow up, add the opposing case, converge on 2–3 conclusions | `references/discussion.md` |
| ② concept | Lesson: 2–3 segments, one check question each, re-explain on a miss, record familiarity | `references/teach-concept.md` |
| ③ article | Guided reading: question and structure first, total time, timed sections, a take-home question | `references/guided-reading.md` |

New understanding from any mode goes into the matching note's `concepts.my_notes_heading`
section (create the section if missing). Keep it to a few lines in the learner's own framing.

## 5. When the reading suggests improving the user's own system

Some articles describe a practice the user could adopt in their own projects (a workflow, a
tool, a review habit). After the guided reading, check whether this one does. If it does:

1. Say in one or two lines which practice maps to which gap, and what would have to change
   because it cannot be copied as-is.
2. Ask for approval with a choice box.
3. On approval, **propose it as a separate session** (in Claude Code, `start_session` with
   `own_initiative`; elsewhere, write the brief to a file and tell the user). Do not start the
   change inside the learning session.

The brief must include: the practice and the gap (with file paths) · the concrete change (files,
how, and why it differs from the article) · acceptance criteria (an observable signal or test)
· how it iterates (when to review, which signal, what to adjust if it misses).

## 6. Quiz list and weekly quiz

- **Quiz list** (`quiz.list_file`): one row per concept taught or picked this week —
  date, concept, why it was picked. Create the file with a header row if missing. Do not add a
  concept twice in the same week.
- **Quiz day** (`quiz.day`): if today is the quiz day and the list has entries not yet
  quizzed, offer the quiz once at the start of /learn ("quiz now, ~10 min / later").
- **Quiz**: five questions, priority list → reviews due (`next_review` ≤ today) → added in the
  last 7 days → low-familiarity foundations. One question at a time; grade right / partial /
  wrong with a short note on what was missing. Question type follows the target level (see
  the rubric in `references/teach-concept.md`). Afterwards write a quiz record if
  `quiz.records_folder` is set, update each concept's familiarity and review dates, and clear
  the list.

Review intervals: wrong → 1 day; partial → 3 days; right → by new familiarity 1→3, 2→7, 3→21,
4→60 days.

## 7. Close

End with one short status in the user's language: what was covered, familiarity changes,
what is on the quiz list, and the next quiz date. If files changed and the project is a git
repo, follow the project's own rule about committing and pushing (ask with a choice box if
it has none). Never push without the user's yes.

## Boundaries

- Never invent what a source says. If the full text could not be read (paywall, fetch failure),
  guide only through what is available and say so; never bypass paywalls or log in for the user.
- Familiarity only changes through a check question, a quiz, or the user explicitly saying
  "I already know this" — never by impression.
- Store summaries and the user's own understanding, not copied passages.
