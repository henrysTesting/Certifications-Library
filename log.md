# Wiki Log

Append-only record of ingests, queries, and maintenance passes.
Format: `## [YYYY-MM-DD] <type> | <title>`

---

## [2026-05-11] ingest | NVIDIA-NCA-GENL-Master-Cheat-Sheet

- Source: `raw/NCA-GENL/NVIDIA-NCA-GENL-Master-Cheat-Sheet.pdf` — 68-page SkillCertPro exam prep guide; all 5 official NCA-GENL weighted domains (Core ML 30%, Data Analysis 14%, Experimentation 22%, Software Development 24%, Trustworthy AI 10%)
- Created source summary: `wiki/NCA-GENL/sources/NVIDIA-NCA-GENL-Master-Cheat-Sheet.md`
- Created 6 concept pages: Feature Engineering, Cross-Validation, Text Embedding Models, Model Scalability and Reliability, Data Privacy and Consent, AI Bias Minimization
- Updated domain pages: LLM Fundamentals (sources: 1→2), Generative AI Concepts (sources: 1→2), RAG and Applications (sources: 1→2), NVIDIA AI Stack (sources: 2→3), Deployment and Optimization (sources: 2→3)
- Updated index.md (Sources: 2→3, Concept pages: 29→35)

---

## [2026-05-08] query | Optimization algorithms for LLM training

- User asked: "Which technique is most effective for dynamically adjusting the learning rate based on gradient variance during optimization?" (Multiple choice: SGD, RMSprop, LARS, Momentum)
- Correct answer: **RMSprop** — dynamically adjusts learning rate based on gradient variance; most effective for non-stationary LLM objectives
- Created concept page: `wiki/NCA-GENL/concepts/Optimization Algorithms for LLMs.md` — covers SGD, Momentum, RMSprop, Adam, LARS with update rules, advantages/limitations, comparison matrix, exam patterns, and scenario-based selection
- Updated index.md (Concept pages: 28→29)

---

## [2026-05-08] query | BERTScore evaluation metric

- User asked: "bertscore"
- Created concept page: `wiki/NCA-GENL/concepts/BERTScore.md` — covers how BERTScore works (embeddings + token-level matching + F-score), comparison with BLEU/ROUGE/cosine similarity, use cases, advantages/limitations, and common exam patterns
- Updated index.md (Concept pages: 27→28)

---

## [2026-05-08] query | Regularization techniques for LLM overfitting

- User asked: "Which of the following strategies is most effective for mitigating the overfitting of a large language model during training?" (Multiple choice: increasing parameters, dropout, reducing batch size, smaller learning rate)
- Correct answer: **Implementing dropout with an appropriate rate during training**
- Created concept page: `wiki/NCA-GENL/concepts/Regularization Techniques for LLMs.md` — covers dropout, weight decay, early stopping, data augmentation, common exam misconceptions, and diagnosis strategies
- Updated index.md (Concept pages: 26→27)

---

## [2026-05-08] query | Perplexity and model fitting

- User asked: "When evaluating an LLM using perplexity, which is true regarding model complexity and underfitting/overfitting?"
- Created concept page: `wiki/NCA-GENL/concepts/Perplexity and Model Fitting.md` — covers perplexity definition, train vs. test comparison, overfitting/underfitting signals, and common exam traps
- Updated index.md (Concept pages: 25→26)

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
