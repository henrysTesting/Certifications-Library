---
description: Ingest a source file from raw/ into the wiki — creates concept pages, updates domains, index, and log
argument-hint: <CERT-ID/filename.md>
---

You are ingesting a source file into the Certifications wiki. Follow the schema defined in `CLAUDE.md` exactly.

## Setup

1. Read `CLAUDE.md` to confirm the current vault schema and active certifications
2. Read `index.md` to understand what concept pages already exist (avoid duplicates)
3. Read `log.md` to see what has already been ingested

## Determine the source path

If $ARGUMENTS is provided, the source file is `raw/$ARGUMENTS`.
If no argument is given, list the contents of `raw/` and ask the user which file to ingest.

Read the source file fully before doing anything else.

## Ingest workflow

Work through these steps in order. Run file writes in parallel where there are no dependencies.

### Step 1 — Source summary page

Create `wiki/<CERT-ID>/sources/<FileName>.md` with:
- Frontmatter: tags, exam, ingested date, domains covered
- A table of sections/modules and what each covers
- A list of key concepts extracted (as `[[Concept Name]]` links — these are the pages you'll create in step 2)

### Step 2 — Concept pages

For each key concept extracted from the source:
- Check `index.md` — if a page already exists for this concept, skip creation (you'll update it in step 3 instead)
- Otherwise create `wiki/<CERT-ID>/concepts/<Concept>.md` with:
  - Frontmatter: tags, exam, domain
  - Clear explanation of the concept
  - Tables, comparisons, or step-by-step breakdowns where useful
  - "Exam Note" section for anything explicitly exam-tested
  - "Related" section linking to other concept pages using bare `[[Page Name]]` links

Aim for depth over brevity — these pages are study material, not stubs.

### Step 3 — Update domain pages

For each domain page in `wiki/<CERT-ID>/domains/` that is touched by this source:
- Add any new topic bullets under "Core Topics"
- Add links to new concept pages under "Concept Pages"
- Add the source under "Sources" as `[[SourceName]] — <brief scope note>`
- Increment `sources:` count in frontmatter

### Step 4 — Update index.md

- Add a row for the new source under the Sources section
- Add a row for each new concept page under the Concepts section
- Update the header counts (`Sources: N | Concept pages: N`)

### Step 5 — Append to log.md

Add an entry in this format:
```
## [YYYY-MM-DD] ingest | <FileName>

- Source: `raw/<CERT-ID>/<FileName>` — <one-line description>
- Created source summary: `wiki/<CERT-ID>/sources/<FileName>.md`
- Created <N> concept pages: <comma-separated list>
- Updated domain pages: <comma-separated list>
- Updated index.md
```

## After ingesting

Report to the user:
- How many concept pages were created
- Which domain pages were updated
- Any concepts mentioned in the source that you flagged as needing their own page but deferred (e.g. too narrow or already covered inline)
- Any gaps or contradictions you noticed relative to existing wiki content
