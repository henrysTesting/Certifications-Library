# Certifications Vault

An Obsidian vault where Claude maintains a study wiki for professional certifications.
You source the material. Claude does the bookkeeping.

---

## Prerequisites

- **[Obsidian](https://obsidian.md/download)** — required to browse the wiki
- **[Claude Code](https://claude.ai/download)** — required to run slash commands
- **[Obsidian Clipper](https://obsidian.md/clipper)** — optional, useful for clipping web content into `raw/`

---

## Setup

1. Clone this repo
2. Open Obsidian → **Open folder as vault** → select the cloned folder
3. Open Claude Code in the same folder

---

## Structure

```
raw/        Drop source files here (notes, PDFs, articles). One subfolder per cert.
wiki/       Claude-maintained wiki. One subfolder per cert.
index.md    Catalog of all wiki pages.
log.md      History of every ingest and operation.
CLAUDE.md   Vault schema — tells Claude how everything works.
```

> `raw/` is gitignored — your source files stay local.

---

## Slash Commands

| Command | Description |
|---|---|
| `/ingest <CERT-ID/file>` | Process a source file into the wiki |
| `/query <question>` | Answer a question using the wiki |
| `/lint` | Health-check the wiki for broken links and gaps |
| `/new-cert <CERT-ID>` | Scaffold the structure for a new certification |

---

## Adding a New Cert

1. Run `/new-cert <CERT-ID>`
2. Drop your source files into `raw/<CERT-ID>/`
3. Run `/ingest <CERT-ID>/<file>`

---

## Current Certs

| ID | Name |
|---|---|
| NCA-GENL | NVIDIA Certified Associate: Generative AI LLMs |
