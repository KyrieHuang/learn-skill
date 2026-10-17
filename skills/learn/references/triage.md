# Triage: is this one piece worth my time?

The user hands over a single article, post, video page or file and asks whether it is worth the
time. Answer on the same three axes as the daily candidates, so the user can pick which kinds of
work to do with this one piece.

Trigger: `/learn <url or path>`, or "is this worth reading", "值不值得看", "幫我判斷這篇".

## 1. Read it

Fetch or open the actual text (same rules as `guided-reading.md`: never judge from the title,
never bypass a paywall). If only part is readable, judge that part and say so. Estimate reading
time from length.

## 2. Judge three axes

For each axis give a verdict — **worth it / maybe / skip** — with a one-line reason tied to the
learner (their work, what they already know, their concept notes) and minutes.

| Axis | The question it answers | Worth it when |
|---|---|---|
| ① Think | Does it raise a question worth discussing? | real tension, a claim to test against the learner's own experience |
| ② Fill in | Does it lean on a concept the learner lacks? | uses a foundation with low familiarity, which would unlock this piece and others |
| ③ Read | Is the full text worth reading, guided? | first-hand, dense, well-argued, or directly about the learner's work; not a summary of something they already have |

Also say in one line what the piece is (who wrote it, what kind of source) and whether it
repeats something already in the notes (link the note).

## 3. Let the user pick

One choice box, `multiSelect: true`, the verdicts in the question field (see
`claude-code-ui.md`), and one option per axis that is not "skip":

- "① Discuss: <the question> · ~15 min"
- "② Learn <concept> first · ~20 min"
- "③ Guided read · ~25 min"
- "Just save the summary" (no session; write a source note through the user's normal flow)

Axes judged "skip" are listed in the question field with their reason but not offered. If all
three are "skip", say so plainly and offer only "save summary / discard".

## 4. Then

- If a time budget is set for today (SKILL.md §1a), check the total and propose a trim.
- Run the picked modes in the recommended order (concept → read → discuss).
- Unpicked but "worth it" axes go into the backlog (`backlog.md`).
