# Driving the choice UI

Tested in the Claude Code desktop app and CLI. These are limits of the interface, not style
preferences; a skill that ignores them silently loses content.

## AskUserQuestion limits

- **At most 4 options per question, at most 4 questions per call.** The client adds an "Other"
  free-text option on its own; never add one yourself.
- Five candidates do not fit one question. Split them **3 + 2** into two questions of the same
  category ("① Questions to think about (1/2)", "(2/2)"), both `multiSelect: true`.
- The time-budget question is its own small box before any candidates.
- More than 16 options in total → a second call. For /learn: call 1 = ①a ①b ②a ②b,
  call 2 = ③a ③b plus any confirmation (low-confidence judgments, "push changes?").
- Each option: a short `label` (the item itself, a few words) and a `description` holding the
  reason and the minutes ("Unlocks 3 of today's notes · ~15 min").
- A recommended option goes first with "(Recommended)" in its label.
- The `header` chip is 12 characters at most.

## Content placed before a choice box gets covered

When a reply ends with a choice box (AskUserQuestion) — or, in the desktop app, with the
end-of-turn wrap-up buttons — the box is drawn over the text that came before it in the same
reply. The user sees the box, not the explanation above it.

So:

- **Anything the user must read goes inside the `question` field** of the box. The question
  field takes several paragraphs; use line breaks. A teaching segment, a reading section, the
  candidate context, the day's one-line stats — all go there.
- The options then answer it: "Done, ask me" / "Explain it another way" / "Go deeper" /
  "Skip this one".
- A check question after a segment is its **own** box (the next call), with the answer choices
  as options.
- Keep text outside boxes to a single line, or none.

## Click, don't type

- Choices, confirmations, gradings, "next item?" → a box.
- Typing only where the user's own words are the point: "explain X in your own words", "what
  do you think about…". Ask those as a plain question at the end of the reply, with no box
  after it, so nothing covers it.
- After the user types an answer, the next box can grade it and continue.

## Other clients

If the client has no choice tool (plain API, other agents, some IDE panels):

- Print the candidates as a numbered list, grouped by category, with reason and minutes on each
  line; ask the user to reply with numbers ("1, 4, 7").
- Put the teaching text normally in the reply; end with the same options as a short list
  ("a) done, ask me  b) another way  c) go deeper").
- Everything else in the skill is unchanged.

If AskUserQuestion fails or is denied once, switch to the fallback for the rest of the session
instead of retrying.
