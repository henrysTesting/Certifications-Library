---
description: Answer a question about certification material using the wiki, with citations
argument-hint: <question>
model: claude-haiku-4-5-20251001
---

You are answering a question about certification study material using the wiki as your knowledge base. Do not rely on general training knowledge alone — ground your answer in the wiki pages.

## The question

The question is: $ARGUMENTS

If no argument was given, ask the user what they want to know.

## Workflow

### Step 1 — Orient with the index

Read `index.md`. Identify which concept pages, domain pages, or source pages are relevant to the question.

### Step 2 — Read relevant pages

Read the pages identified in step 1. If a page links to another page that seems relevant, read that too (max 2 hops).

### Step 3 — Synthesize the answer

Write a clear, well-structured answer that:
- Directly addresses the question
- Cites wiki pages inline using `[[Page Name]]` notation
- Uses tables or comparisons where they help clarity
- Highlights anything explicitly marked as exam-relevant in the pages

If the answer requires information not yet in the wiki, say so clearly and note what source would fill the gap.

### Step 4 — Offer to save

If the answer is substantial (more than a quick fact), ask the user:
> "Want me to save this as a wiki page?"

If yes, create `wiki/<CERT-ID>/concepts/<Topic>.md` with the answer content, add it to `index.md`, and append a `query` entry to `log.md`.
