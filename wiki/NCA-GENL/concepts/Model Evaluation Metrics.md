---
tags: [concept, evaluation, metrics]
exam: NCA-GENL
domain: Experimentation
---

# Model Evaluation Metrics

## Text Generation / NLP Metrics

| Metric | Full Name | Measures | Use Case |
|--------|-----------|----------|----------|
| **BLEU** | Bilingual Evaluation Understudy | Precision — how much of the generated output appears in reference translations (n-gram overlap) | Machine translation |
| **ROUGE** | Recall-Oriented Understudy for Gisting Evaluation | Recall — how much of the reference content appears in the generated summary | Summarization |
| **Cosine Similarity** | — | Similarity between two text vectors (0=unrelated, 1=identical) | Semantic search, text similarity |

### ROUGE Variants
- **ROUGE-N**: n-gram overlap between generated and reference text
- **ROUGE-L**: longest common subsequence

### BLEU vs. ROUGE Memory Aid
- **BLEU = precision** (does the output match the reference?)
- **ROUGE = recall** (does the reference appear in the output?)

## Classification Metrics

| Metric | Formula / Definition |
|--------|---------------------|
| **Precision** | Of all predicted positives, how many were actually positive |
| **Recall** | Of all actual positives, how many did the model catch |
| **F1 Score** | Harmonic mean of precision and recall; use for imbalanced classes |
| **AUC-ROC** | Area under ROC curve; measures discriminative power |
| **R²** | Proportion of variance explained; 1.0 = perfect fit (regression) |

## LLM Benchmarks

| Benchmark | Tests |
|-----------|-------|
| GLUE / SuperGLUE | General NLP task suite |
| MMLU | Breadth of knowledge across many domains |
| HellaSwag | Commonsense reasoning |
| HumanEval | Code generation |

## Multilingual Evaluation

Robust evaluation across diverse languages requires dedicated multilingual benchmarks in addition to English-only suites.

| Benchmark | Full Name | Tests |
|-----------|-----------|-------|
| **XNLI** | Cross-lingual Natural Language Inference | Natural language inference across 15 languages; tests cross-lingual transfer |
| **GLUE** (see above) | — | General NLP; English-focused |

### Why Combine Benchmarks?

- A single benchmark only tests one dimension of performance
- GLUE alone = strong English task coverage, weak multilingual signal
- XNLI alone = cross-lingual coverage, but limited task diversity
- **Combining GLUE + XNLI** = robust evaluation across both diverse tasks and diverse languages
- Best practice for LLMs intended for real-world, multilingual deployment

### Exam Note

- When asked about evaluation for **"diverse languages and contexts"**, the answer is a **combination of benchmarks** — e.g., GLUE (task diversity) + XNLI (language diversity)
- Relying on a single metric or monolingual corpus is insufficient for robust multilingual evaluation

## Evaluation Strategies

| Strategy | When to Use |
|----------|-------------|
| Train/Val/Test split | Standard; never use test data during training |
| Cross-validation | When test data is unavailable; averages across k folds |
| A/B testing | Two model variants served to different user groups; compare real-world outcomes |

## Related

- [[Fine-Tuning and LoRA]]
- [[RAG]]
