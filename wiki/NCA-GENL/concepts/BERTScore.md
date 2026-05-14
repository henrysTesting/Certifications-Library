---
tags: [concept, evaluation, metrics, semantic]
exam: NCA-GENL
domain: Experimentation
sources: 0
---

# BERTScore

## Overview

BERTScore is a modern evaluation metric for text generation that measures semantic similarity between generated and reference text using contextual embeddings from pre-trained language models (typically BERT).

Unlike surface-level metrics like BLEU and ROUGE, BERTScore captures semantic meaning rather than exact word overlap, making it more aligned with human judgment.

## How BERTScore Works

### Step 1: Generate Embeddings

- Tokenize both generated and reference text
- Pass through a pre-trained language model (BERT, RoBERTa, etc.) to get contextual embeddings
- Each token has a dense vector representation capturing its semantic context

### Step 2: Compute Similarity

For each token in the generated text:
- **Greedy matching:** Find the most similar token in the reference text (highest cosine similarity)
- **Soft matching (optional):** Average similarity to top-k reference tokens for softer scoring

### Step 3: Compute F-Score

| Component | Calculation | Meaning |
|-----------|-------------|---------|
| **Precision** | Average similarity from generated → reference | Did the model generate relevant content? |
| **Recall** | Average similarity from reference → generated | Did the model capture all reference content? |
| **F-Score** | Harmonic mean of precision and recall | Overall similarity (0=unrelated, 1=perfect) |

## BERTScore vs. Traditional Metrics

| Metric | Approach | Strength | Weakness |
|--------|----------|----------|----------|
| **BLEU** | N-gram overlap (precision) | Fast; standard; language-agnostic | Ignores semantics; penalizes paraphrases |
| **ROUGE** | N-gram overlap (recall) | Good for summarization | Ignores semantics; penalizes paraphrases |
| **Cosine Similarity** | Embedding similarity (entire sequences) | Semantic awareness | Treats entire text as single vector; loses word-level detail |
| **BERTScore** | Token-level semantic matching | Semantic + word-level detail; captures paraphrases | Requires pre-trained model; slower than n-gram metrics |

### Example

**Reference:** "The cat sat on the mat."  
**Generated:** "A feline was resting on the carpet."

- **BLEU:** Very low (different words, even though meaning is similar)
- **ROUGE:** Very low (minimal word overlap)
- **BERTScore:** High (semantic correspondence: cat↔feline, sat↔resting, mat↔carpet)

## When to Use BERTScore

| Use Case | Recommendation |
|----------|-----------------|
| Machine translation | ✅ BERTScore (captures paraphrases) |
| Text summarization | ✅ BERTScore (semantic fidelity matters more than word overlap) |
| Paraphrase detection | ✅ BERTScore (designed for semantic similarity) |
| Quick baseline evaluation | ⚠️ BLEU/ROUGE (faster; acceptable for internal testing) |
| Multilingual evaluation | ✅ Multilingual BERT (mBERT, XLM-R) |
| Real-time scoring | ❌ BERTScore (slower than n-gram metrics) |

## Advantages

- **Semantic awareness:** Captures meaning, not just surface-level word matches
- **Paraphrase-friendly:** Gives credit for semantically equivalent variations
- **Alignment with human judgment:** Correlates better with human evaluation than BLEU/ROUGE
- **Flexible embeddings:** Can use any pre-trained language model (BERT, RoBERTa, DistilBERT, etc.)
- **Multilingual:** Multilingual models enable cross-language evaluation

## Limitations

- **Computational cost:** Requires forward passes through a large language model; slower than BLEU/ROUGE
- **Model dependency:** Results vary based on which pre-trained model is used
- **Requires reference text:** Cannot score generations without gold-standard references
- **Less stable for short texts:** Token-level matching is less reliable on very short sequences
- **Not interpretable:** Doesn't provide per-word feedback like BLEU does

## Comparison Matrix

| Feature | BLEU | ROUGE | BERTScore |
|---------|------|-------|-----------|
| Semantic understanding | ❌ | ❌ | ✅ |
| Fast computation | ✅ | ✅ | ❌ |
| Paraphrase-aware | ❌ | ❌ | ✅ |
| Interpretable | ✅ | ✅ | ⚠️ (black-box) |
| Multilingual support | ✅ (language-agnostic) | ✅ (language-agnostic) | ✅ (with mBERT) |
| Human correlation | ⚠️ (moderate) | ⚠️ (moderate) | ✅ (high) |

## Common Exam Patterns

| Question Pattern | Answer |
|------------------|--------|
| "Which metric is best for evaluating text with synonyms and paraphrases?" | **BERTScore** (semantic matching > surface overlap) |
| "Which metric correlates most strongly with human judgment?" | **BERTScore** (> BLEU/ROUGE) |
| "Which metric requires a pre-trained language model?" | **BERTScore** (BLEU/ROUGE are model-agnostic) |
| "Which metric is fastest for quick evaluation?" | **BLEU/ROUGE** (not BERTScore) |
| "Which metric works best for machine translation?" | **BERTScore** (captures paraphrases) |

## Related

- [[Model Evaluation Metrics]]
- [[Embeddings]]
- [[Transformer Architecture]]
- [[BERT]]
