# Wiki Log

Append-only record of ingests, queries, and maintenance passes.
Format: `## [YYYY-MM-DD] <type> | <title>`

---

## [2026-04-24] query | RNN fundamentals and use cases

- User asked: "What is RNN? and its best use case"
- Created concept page: `wiki/NCA-GENL/concepts/RNN.md` — covers RNN definition, mechanism, variants (LSTM/GRU/BiRNN), best use cases, advantages/limitations, and comparison with transformers
- Updated index.md (Concept pages: 24→25)

---

## [2026-04-24] update | LLM Deployment Strategies — new concept page

- Created `wiki/NCA-GENL/concepts/LLM Deployment Strategies.md`
- Covers: blue-green, canary, rolling updates, hotfix anti-pattern, Triton model versioning
- Updated index.md (Concept pages: 23→24)

---

## [2026-04-24] update | Model Evaluation Metrics — added multilingual benchmarks

- Updated `wiki/NCA-GENL/concepts/Model Evaluation Metrics.md`
- Added "Multilingual Evaluation" section covering XNLI and cross-lingual benchmarks
- Added exam note: GLUE + XNLI combination is the correct answer pattern for diverse-language evaluation questions

---

## [2026-04-24] ingest | Cheat Sheet for NVIDIA GenAI Ecosystem.pdf

- Source: `raw/NCA-GENL/Cheat Sheet for NVIDIA GenAI Ecosystem.pdf` — NVIDIA GenAI ecosystem reference covering GPU hardware, core libraries, LLM software stack, profiling tools, and cloud platforms
- Created source summary: `wiki/NCA-GENL/sources/Cheat Sheet for NVIDIA GenAI Ecosystem.md`
- Created 9 concept pages: GPU Architecture and Hardware, NVIDIA Compute Systems, NeMo Framework, Megatron-LM, TensorRT-LLM, FlashAttention, vLLM and PagedAttention, NVIDIA Profiling Tools, NVIDIA Platforms and Services
- Updated domain pages: NVIDIA AI Stack (sources: 1→2), Deployment and Optimization (sources: 1→2)
- Updated index.md (Sources: 1→2, Concept pages: 14→23)

---

## [2026-04-24] update | Vault restructure — cert-namespaced layout

- Moved all wiki pages into `wiki/NCA-GENL/` (exams, domains, concepts, sources)
- Moved raw source into `raw/NCA-GENL/`
- Fixed all internal links to use bare `[[Page Name]]` format (Obsidian resolves by filename)
- Fixed `index.md` links to match new structure
- Rewrote `CLAUDE.md` as a full operational schema: directory layout, conventions, ingest/query/lint/add-cert workflows

---

## [2026-04-24] ingest | GenAINotes.md

- Source: `raw/GenAINotes.md` — personal study notes, 769 lines
- Coverage: Modules 1–10 (skipping 7) + full 5-domain exam supplement
- Created source summary: `wiki/sources/GenAINotes.md`
- Created 20 concept pages:
  - Transformer Architecture, Attention Mechanism, Tokenization, Embeddings, BERT
  - Activation Functions, Backpropagation
  - Prompt Engineering, Fine-Tuning and LoRA, RLHF, Diffusion Models
  - NVIDIA Ecosystem, Triton Inference Server, Quantization, Distributed Deep Learning
  - RAG, Model Evaluation Metrics, Trustworthy AI
  - HuggingFace Transformers, Python Libraries
- Updated all 5 domain pages with source links and expanded topic coverage
- Updated index.md (20 concept pages, 1 source)

---

## [2026-04-24] init | NCA-GENL vault setup

- Created directory structure: `raw/`, `wiki/concepts/`, `wiki/domains/`, `wiki/sources/`, `wiki/exams/`
- Scaffolded exam page: `wiki/exams/NCA-GENL.md`
- Scaffolded 5 domain pages covering all NCA-GENL exam domains
- Created `index.md` and `log.md`
- Ready to ingest personal notes
