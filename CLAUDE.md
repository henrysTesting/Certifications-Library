# Certifications Vault — Schema

This is the operational schema for the Certifications Obsidian vault. It tells any AI assistant how the vault is structured, what the conventions are, and how to perform the standard operations. Read this file at the start of every session.

---

## Purpose

A persistent, LLM-maintained wiki for studying professional certifications. The human sources material and asks questions. The AI writes and maintains all wiki content — summaries, concept pages, cross-references, and the index.

---

## Directory Structure

```
Certifications/
├── raw/
│   └── <CERT-ID>/          ← source files per cert (immutable — never modify)
├── wiki/
│   └── <CERT-ID>/          ← all wiki content for that cert
│       ├── exams/          ← one overview page per cert
│       ├── domains/        ← one page per exam domain/objective area
│       ├── concepts/       ← one page per concept, tool, or topic
│       └── sources/        ← one summary page per ingested source
├── index.md                ← catalog of all wiki pages (update on every ingest)
├── log.md                  ← append-only history of all operations
└── CLAUDE.md               ← this file
```

**Active certifications:**
- `NCA-GENL` — NVIDIA Certified Associate: Generative AI LLMs

---

## File Conventions

### Frontmatter (all wiki pages)

```yaml
---
tags: [<type>, <topic>, ...]   # type = exam | domain | concept | source
exam: <CERT-ID>                # e.g. NCA-GENL
domain: <Domain Name>          # primary domain this page belongs to (concepts/sources only)
sources: <N>                   # number of sources referenced (domain pages only)
ingested: YYYY-MM-DD           # date ingested (source pages only)
last_updated: YYYY-MM-DD       # date last modified (exam pages only)
---
```

### Internal Links

Use bare `[[Page Name]]` links — Obsidian resolves by filename across the vault.
Do **not** use path-prefixed links like `[[concepts/X]]` or `[[wiki/NCA-GENL/concepts/X]]`.

### Index Entries

One line per page: `| [[Page Name]] | one-line summary |`
Organized by section: Exams → Domains → Concepts → Sources.
Update the header count (`Sources: N | Concept pages: N`) on every ingest.

### Log Entries

Format: `## [YYYY-MM-DD] <type> | <title>`
Types: `init`, `ingest`, `query`, `lint`, `update`
Each entry lists what files were created, updated, or removed.

---

## Operations

### Ingest

Triggered when the user says "ingest" or drops a file in `raw/<CERT-ID>/`.

1. Read the source file
2. Discuss key takeaways with the user if they want (ask first for large sources)
3. Create `wiki/<CERT-ID>/sources/<SourceName>.md` — summary, module/section coverage, list of extracted concepts
4. For each key concept not yet in the wiki: create `wiki/<CERT-ID>/concepts/<Concept>.md`
5. Update relevant `wiki/<CERT-ID>/domains/*.md` — add topic bullets, link to new concept pages, update `sources:` count in frontmatter
6. Update `index.md` — add new concept and source rows, update header counts
7. Append an entry to `log.md`

A single source typically touches 10–20 files. Run writes in parallel where possible.

### Query

Triggered when the user asks a question about the material.

1. Read `index.md` to identify relevant pages
2. Read those pages
3. Synthesize an answer with citations to wiki pages
4. If the answer is substantial and reusable, offer to file it as a new concept page

### Lint

Triggered when the user says "lint" or "health check".

Check for:
- Broken `[[links]]` — pages referenced but not yet created
- Orphan pages — no inbound links
- Domain pages with zero sources
- Concepts mentioned in notes but lacking their own page
- Outdated frontmatter counts

Report findings and ask the user which to fix.

### Add a New Certification

When the user says they want to study for a new cert:

1. Create `raw/<CERT-ID>/` for source files
2. Create `wiki/<CERT-ID>/exams/<CERT-ID>.md` — exam overview and domain table
3. Create `wiki/<CERT-ID>/domains/<Domain>.md` for each exam domain
4. Add the cert to the "Active certifications" list in this file
5. Update `index.md` with a new Domains section for the cert
6. Append an `init` entry to `log.md`

---

## Shared Concepts Across Certs

Some concepts (e.g. Transformers, Backpropagation, Python Libraries) may apply to multiple certifications. When this occurs:

- Keep the concept page under whichever cert introduced it
- Link to it from the other cert's domain pages using a bare `[[Page Name]]` link
- Add a note in the concept page frontmatter if it spans multiple certs: `exams: [NCA-GENL, <OTHER>]`

---

## Quick Reference

| Operation | Trigger phrase |
|-----------|---------------|
| Ingest a source | "Ingest raw/" or "process this file" |
| Answer a question | Any content question |
| File an answer as a page | "Save this as a wiki page" |
| Health check | "Lint the wiki" or "health check" |
| Add a cert | "I want to study for <CERT>" |
| Update the schema | "Update CLAUDE.md" |
