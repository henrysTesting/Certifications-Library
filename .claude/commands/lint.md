---
description: Health-check the wiki — find broken links, orphan pages, missing concepts, and stale counts
argument-hint: [CERT-ID]
---

You are performing a health check on the Certifications wiki. Your job is to find problems and report them as a prioritized punch list — not to fix everything automatically.

## Scope

If $ARGUMENTS is provided, limit the check to `wiki/$ARGUMENTS/`.
Otherwise check all certs in `wiki/`.

Also always check the top-level `index.md` and `log.md`.

## Checks to run

Run all of these. Collect findings before reporting.

### 1. Broken links
Scan every wiki page for `[[Page Name]]` links. For each link, verify a file with that name exists somewhere in `wiki/`. Report any that don't resolve.

### 2. Orphan pages
List all concept pages. For each one, check whether any other page links to it. Report pages with zero inbound links — they can't be reached from anywhere in the wiki.

### 3. Domain pages with no sources
Check each `domains/*.md` — report any where the Sources section is empty or the `sources:` frontmatter count is 0.

### 4. Concepts mentioned but not paged out
Scan domain pages for topic bullets that don't have a corresponding `[[Link]]` to a concept page. These are concepts covered in domains but without their own dedicated page.

### 5. Index count drift
Compare the actual number of concept pages and source pages in `wiki/` against the counts in `index.md`'s header. Report any mismatch.

### 6. Missing index entries
Check that every file in `wiki/<CERT-ID>/concepts/` and `wiki/<CERT-ID>/sources/` has a corresponding row in `index.md`. Report any missing.

### 7. Raw files not yet ingested
List files in `raw/` that don't have a matching source page in `wiki/<CERT-ID>/sources/`. These are sources dropped in but never processed.

## Report format

Present findings as a punch list grouped by severity:

**Must fix** — broken links, index drift, un-ingested raw files
**Should fix** — orphan pages, missing index entries
**Nice to fix** — unpaged concepts, empty domain sources

For each finding, give the file path and the specific issue.

End with: "Which of these do you want me to fix?"
Only fix items the user explicitly approves.
