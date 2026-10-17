# Teaching a concept

Goal: move the learner up one familiarity level, verified, in 10–15 minutes.

## Familiarity scale (0–4)

| Level | Name | The learner can… | Check question that proves it |
|---|---|---|---|
| 0 | Not met | — (only seen the word in a note) | — |
| 1 | Heard of | recognize the term, not explain it | "Which of these is X?" |
| 2 | Basic | explain what it is and why it matters in their own words | "Explain X in your own words" / a situation where they must pick X |
| 3 | Working | compare it with related concepts, apply it to a new case | "X vs Y — what differs?" / "Should you use X here?" |
| 4 | Expert | name its limits and controversies, teach it, critique a claim about it | "What is wrong with this claim?" / "Where does X break?" |

Multiple-choice checks prove recognition and application, not explanation. If the learner got
every multiple-choice check right but never explained it in their own words, record level 2
with a note "explanation not yet verified" and put it on the quiz list; the quiz confirms or
drops it to 1.

## Before you start

1. Read the concept note (`concepts.folder`): current familiarity, parents, past quiz rows,
   the learner's own notes. Do not re-teach what a past row shows they already have.
2. Find the **entry point**: a thing the learner has actually run into. Use the `learner`
   section of the config (their work, systems, past confusions) and today's material. A
   learner who builds things but lacks theory should start from "you saw this happen in your
   own setup — here's why"; a learner from another field should get an analogy from that
   field.
3. Plan 2–3 segments, each one idea. Typical shape: what it is (through the entry point) →
   how it works (the one mechanism that matters) → the trade-off or where it shows up next.

Say up front: "About N minutes, M short parts."

## Each segment

- Put the segment in the choice box's question field (see `claude-code-ui.md`). Short
  paragraphs, one idea, no stacked jargon; introduce at most one new term per segment and
  define it in plain words the first time.
- Options: "Got it, check me" / "Explain it another way" / "Go deeper" / "Skip".
- Then a check question in its own box: one question, 3–4 options, one clearly right, the
  wrong ones being the misconceptions people actually have.
- **Wrong answer** → do not just reveal the answer. Say what the chosen option gets right and
  where it slips, re-explain from a different angle (new analogy, concrete numbers, a
  counter-example), then ask a fresh check question on the same idea.
- Two misses on the same idea → slow down: split the idea into smaller steps, or go down to
  its parent concept first (and say you are doing so).

## After the last segment

1. Decide the new familiarity from the evidence, using the table above. Never round up.
2. Update the concept note:
   - `concepts.familiarity_field`, `last_review` = today, `next_review` by the interval rule
     in SKILL.md §6.
   - Add a row to the quiz record table (`concepts.quiz_table_heading`). Default columns:
     `| Date | Question | Result | Familiarity |` — follow the existing table if the note
     already has one, e.g. `| 2026-03-02 | Lesson checks (3 multiple choice): … | 3/3 right | 0 → 2 (explanation not yet verified) |`.
   - A few lines in the learner's own framing under `concepts.my_notes_heading`.
3. Add the concept to the quiz list (if not already there this week).
4. Offer, as a choice: "next item / one more level on this / stop here", each with minutes.

## Do not

- Do not dump the whole explanation in one message.
- Do not ask "do you understand?" — ask a question that shows it.
- Do not raise familiarity because the learner said "makes sense".
