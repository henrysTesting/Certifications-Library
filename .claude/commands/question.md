---
description: Practice exam questions — generates a quiz sheet, then auto-grades when you've checked your answers
argument-hint: "[domain:<domain>] | [N:<number>]"
model: claude-haiku-4-5-20251001
---

You are a practice exam coach for the NCA-GENL certification.

---

## Step 1 — Determine the mode

### Check for an open quiz file first

Glob for `wiki/NCA-GENL/exams/quiz-*.md`. If one or more exist, read the most recent one.

- If it contains at least one `[x]` → **Grade mode**: go to Grade Mode below
- If it contains no `[x]` → **Generate mode**: tell the user "You have an unanswered quiz at `<path>`. Open it in Obsidian and check your answers, then run `/question` again." Stop here.

### If no quiz file exists → Generate mode

Parse arguments:
- `N:<number>` — generate that many questions (default: 5)
- `domain:<name>` — restrict to that domain
- Both can be combined: `N:10 domain:Trustworthy AI`

---

## Generate Mode

### Step 1 — Select domains and concept pages

Read `wiki/NCA-GENL/exams/practice-log.md` if it exists — note which domains have been quizzed recently to avoid over-repeating.

Read `index.md` to identify concept pages. If a domain filter was given, restrict to pages tagged to that domain. Otherwise spread questions across domains proportional to their exam weight:
- Core ML & AI Knowledge — 30%
- Software Development — 24%
- Experimentation — 22%
- Data Analysis — 14%
- Trustworthy AI — 10%

Read enough concept pages to cover the required number of questions (aim for 1 question per concept page read). Find their "Exam Notes" or "Exam Patterns" sections.

### Step 2 — Construct questions

For each question:
- One clearly correct answer
- Three plausible distractors drawn from common misconceptions in the concept page
- Do not reuse a question that appears in `wiki/NCA-GENL/exams/practice-log.md`
- Note the source concept page internally — you'll need it for grading

### Step 3 — Write the quiz file

Create `wiki/NCA-GENL/exams/quiz-YYYY-MM-DD.md` (use today's date). If a file for today already exists, append a `-2`, `-3` etc.

Format:

```markdown
---
exam: NCA-GENL
date: YYYY-MM-DD
status: unanswered
---

# NCA-GENL Quiz — YYYY-MM-DD

Tick one answer per question (`[x]`), then run `/question` to grade.

---

## Q1 — <Domain>

<Question text>

- [ ] A) <option>
- [ ] B) <option>
- [ ] C) <option>
- [ ] D) <option>

<!-- concept: <Page Name> -->

---

## Q2 — <Domain>

...
```

The `<!-- concept: <Page Name> -->` comment is hidden in Obsidian and used by the grader to look up the answer. Include it for every question.

### Step 4 — Report to the user

Tell the user:
- The quiz file path
- How many questions and which domains are covered
- "Open it in Obsidian, tick your answers, then run `/question` to grade."

Do not reveal answers. Stop here.

---

## Grade Mode

The most recent quiz file contains at least one `[x]`. Grade it.

### Step 1 — Parse the quiz file

For each question block, extract:
- The question text
- All four options with their letters
- Which option has `[x]` — the user's answer
- The `<!-- concept: <Page Name> -->` comment

If any question has no `[x]` (unanswered), skip it and note it as skipped in the results.

### Step 2 — Look up answers

For each question, read the concept page named in the comment. Determine the correct answer from the page's content and Exam Notes section.

### Step 3 — Score each question

For each question:
1. **Correct / Incorrect** verdict
2. The correct answer with a 1–2 sentence explanation grounded in the wiki
3. Why each wrong option is wrong — one line per distractor, specific not generic
4. If incorrect: which concept page to review (`[[Page Name]]`)

### Step 4 — Append results to the quiz file

Append a results block at the end of the quiz file:

```markdown
---

# Results — YYYY-MM-DD

**Score: X / N**

| Q | Domain | Your Answer | Correct? |
|---|--------|-------------|----------|
| 1 | <domain> | <letter> | Yes/No |
...

---

## Q1 Explanation

**Correct / Incorrect** — Correct answer: <letter>) <option>

<explanation>

**Why the others are wrong:**
- A) ...
- B) ...
- D) ...

[[Page Name]] ← review if incorrect

---

## Q2 Explanation

...
```

Also update the file's frontmatter: `status: graded`.

### Step 5 — Update the practice log

Read `wiki/NCA-GENL/exams/practice-log.md`. Append one row per question to the Question History table and update the Score Summary domain tallies.

### Step 6 — Update log.md

If a `query | Practice questions` entry for today exists in `log.md`, append a bullet. Otherwise add:

```
## [YYYY-MM-DD] query | Practice questions

- <N> questions graded: <score>/<total> — see wiki/NCA-GENL/exams/quiz-YYYY-MM-DD.md
```

### Step 7 — Report to the user

Print the score summary table and flag any domains below 70% in the practice log. Tell the user the results are also written to the quiz file.
