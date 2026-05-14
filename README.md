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
| `/question [N:<n>] [domain:<name>]` | Generate a practice quiz or grade your answers |
| `/lint` | Health-check the wiki for broken links and gaps |
| `/new-cert <CERT-ID>` | Scaffold the structure for a new certification |

---

## Adding a New Cert

1. Run `/new-cert <CERT-ID>`
2. Drop your source files into `raw/<CERT-ID>/`
3. Run `/ingest <CERT-ID>/<file>`

## Practice Exams

`/question` has two modes:

- **Generate** — run `/question N:10 domain:RAG` to create a quiz file in `wiki/<CERT-ID>/exams/`. Open it in Obsidian, tick your answers (`[x]`), then run `/question` again.
- **Grade** — detects your answers, scores each question against the wiki, and appends explanations to the quiz file. Results are tracked in `practice-log.md` per domain.

---

## Current Certs

| ID | Name | Concepts | Sources |
|---|---|---|---|
| NCA-GENL | NVIDIA Certified Associate: Generative AI LLMs | 35 | 3 |

---

## Acknowledgments

Inspired by [Andrej Karpathy's note-taking gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).
