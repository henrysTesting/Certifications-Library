---
description: Scaffold the full wiki structure for a new certification
argument-hint: <CERT-ID>
---

You are adding a new certification to the Certifications vault. Follow the schema in `CLAUDE.md` exactly.

## Determine the cert

If $ARGUMENTS is provided, the cert ID is $ARGUMENTS (e.g. `AWS-SAA`, `COMPTIA-SEC`, `AZ-900`).
If no argument is given, ask the user for:
1. The cert ID/code (used as the folder name)
2. The full cert name
3. The exam domains/objective areas and their approximate weights (check the official exam guide if the user has it, or ask them to list the domains)

## Scaffold workflow

### Step 1 — Raw folder
Create `raw/<CERT-ID>/` (create a `.gitkeep` placeholder so the folder exists).

### Step 2 — Exam overview page
Create `wiki/<CERT-ID>/exams/<CERT-ID>.md` with:
- Frontmatter: tags, cert, last_updated
- Exam name, provider, and a one-line description
- A domain table: `| [[Domain Name]] | brief description |` for each exam domain
- A "Key Resources" section (official exam guide URL if known, else a placeholder)
- A "Study Notes" section linking to `[[index]]` and `[[log]]`

### Step 3 — Domain pages
For each exam domain, create `wiki/<CERT-ID>/domains/<Domain Name>.md` with:
- Frontmatter: tags, exam, sources: 0
- A "Core Topics" section listing the key topics for that domain (use official exam objectives if available, otherwise make reasonable stubs based on the domain name)
- Empty "Concept Pages" section
- Empty "Sources" section

### Step 4 — Update index.md
Add a new Domains section for the cert:
```
## Domains (<CERT-ID>)

| Page | Weight | Summary |
|------|--------|---------|
| [[Domain Name]] | XX% | one-line summary |
...
```

### Step 5 — Update CLAUDE.md
Add the new cert to the "Active certifications" list under the Directory Structure section.

### Step 6 — Append to log.md
```
## [YYYY-MM-DD] init | <CERT-ID> vault setup

- Created `raw/<CERT-ID>/`
- Scaffolded exam page: `wiki/<CERT-ID>/exams/<CERT-ID>.md`
- Scaffolded <N> domain pages: <comma-separated list>
- Updated index.md and CLAUDE.md
- Ready to ingest sources
```

## After scaffolding

Report to the user:
- What was created
- The next step: "Drop your source files into `raw/<CERT-ID>/` and run `/ingest` to start building the wiki."
