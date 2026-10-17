# /learn — a study companion for Claude Code

[English](#english) · [繁體中文](#繁體中文)

## English

You save articles, notes and links faster than you learn from them. `/learn` turns that pile
into a short, focused session:

1. It asks how much time you have today, then reads **your** notes and reading list (only the
   folders you point it at).
2. It offers three kinds of candidates — **a question worth thinking about**, **a foundational
   concept to fill in**, **an article worth reading** — five honest picks each, every one with a
   reason and a time estimate.
3. You pick by clicking (multi-select). It never decides for you — but if you pick more than
   your time budget, it proposes what to trim and asks.
   Good picks you skip are kept in a backlog and come back on a thinner day; after three skips
   they retire.
4. It works through your picks one at a time:
   - **Question → discussion.** Asks your view first, probes, brings the opposing case,
     converges on 2–3 conclusions.
   - **Concept → a short lesson.** Two or three segments, a check question after each, a new
     explanation when you miss, familiarity recorded on a 0–4 scale.
   - **Article → guided reading.** The question it answers and its structure first, total time,
     minutes per section, a take-home question at the end.
5. Concepts go on a weekly quiz list; on your quiz day it offers a five-question quiz with
   spaced review dates.
6. If an article suggests a better way to run your own projects, it proposes the change with
   acceptance criteria — and does it in a separate session only after you approve.

Hand it a single article instead (`/learn <link>`, "is this worth my time?") and it judges that
one piece on the same three axes — worth thinking about, a concept to fill in first, worth
reading in full — each with a reason and minutes, and you tick the ones you want.

Works with any folder of Markdown notes; especially at home in an Obsidian vault.

### Install

```text
/plugin marketplace add KyrieHuang/learn-skill
/plugin install learn@learn-skill
```

Or from a local clone:

```bash
claude plugin marketplace add /path/to/learn-skill
claude plugin install learn@learn-skill
```

### Configure

Copy the template in [`skills/learn/references/config-template.md`](skills/learn/references/config-template.md)
to `.claude/learn.config.md` in your notes project and edit it: language, where your notes and
reading list live, your concept-note fields, your quiz day, and — most important — a few lines
about who you are and how you like to be taught. No config? `/learn` asks three quick questions
and writes one for you.

### Try it on the example

[`examples/`](examples/) is a small fictional vault (a baker learning about loans and chatbots)
with its own config:

```bash
cd examples
claude
```

Then type `/learn`.

### Notes on the interface

The skill is written around tested limits of Claude Code's choice boxes (4 options per
question, 4 questions per box; text before a box gets covered, so reading material goes inside
the box). Details and a fallback for clients without choice boxes:
[`claude-code-ui.md`](skills/learn/references/claude-code-ui.md).

### License

MIT.

---

## 繁體中文

存下來的文章、筆記、連結，永遠比讀懂的多。`/learn` 把這堆東西變成一段短而專注的學習：

1. 先問你今天有多少時間，再讀**你**指定的筆記資料夾和閱讀清單。
2. 給三類候選：**值得想的一題**、**該補的底層概念**、**值得讀完的一篇**，每類 5 個真心推薦，各附推薦理由和預估時間。
3. 你用點的複選，它不替你決定；勾得超過時間預算時，它會提出怎麼取捨、跟你確認。沒選的好候選會留在候選池，素材少的日子再拿出來；推過三次都沒選就退場。
4. 一次陪你做一項：
   - **題目 → 討論**：先問你的看法，再追問、補反方，最後收斂成 2–3 個結論。
   - **概念 → 教一輪**：分 2–3 段，每段後一個確認題，答錯換個講法，結束依 0–4 熟悉度標準記錄。
   - **文章 → 導讀**：先講這篇要回答什麼、結構怎麼走、整篇多久，逐段標時間帶讀，最後留一個帶走的問題。
5. 學過的概念進「本週待測」，每週固定一天出 5 題，依結果排下次複習。
6. 讀到可以改進你自己系統的做法時，提出改進辦法和驗收標準，你批准後才另開對話動手。

也可以只丟一篇文章（`/learn <連結>`、「這篇值不值得看」），它會從「值得想／該先補的概念／值得讀全文」三個面向各給判斷、理由和時間，你勾要做哪幾件。

任何 Markdown 筆記資料夾都能用，Obsidian vault 最合適。

### 安裝

```text
/plugin marketplace add KyrieHuang/learn-skill
/plugin install learn@learn-skill
```

本機 clone 的話：

```bash
claude plugin marketplace add /path/to/learn-skill
claude plugin install learn@learn-skill
```

### 設定

把 [`config-template.md`](skills/learn/references/config-template.md) 裡的範本複製到筆記專案的 `.claude/learn.config.md` 再改：語言、筆記和閱讀清單在哪、概念筆記的欄位、測驗日，以及最重要的：幾行關於你是誰、喜歡怎麼被教。沒有設定檔的話，`/learn` 會問三個問題幫你建一份。

### 用範例試跑

[`examples/`](examples/) 是一個小小的虛構 vault（一位烘焙店老闆在學貸款利率和聊天機器人），自帶設定檔：

```bash
cd examples
claude
```

輸入 `/learn` 即可。

### 介面限制

這個 skill 照 Claude Code 選項框實測過的限制寫成（一題最多 4 個選項、一次最多 4 題；選項框會蓋住它前面的文字，所以要讀的內容放進框裡）。細節和沒有選項框的客戶端怎麼退而求其次，見 [`claude-code-ui.md`](skills/learn/references/claude-code-ui.md)。

### 授權

MIT。
