---
tags: [concept, bert, transformer, encoder]
exam: NCA-GENL
domain: LLM Fundamentals
---

# BERT (Bidirectional Encoder Representations from Transformers)

Encoder-only transformer that reads text bidirectionally — uses both left and right context simultaneously.

## Pre-Training Tasks

| Task | Description |
|------|-------------|
| **Masked Language Modeling (MLM)** | Randomly mask tokens; model predicts the masked tokens |
| **Next Sentence Prediction (NSP)** | Predict if sentence B follows sentence A in the original text |

## Architecture

- Encoder-only (no decoder)
- Bidirectional: all tokens attend to all other tokens simultaneously
- Contrast with GPT: decoder-only, autoregressive, left-to-right only

## Fine-Tuned For

- Text classification (sentiment, topic)
- Named Entity Recognition (NER)
- Question answering
- Author attribution
- Semantic similarity

## BERT vs. GPT

| | BERT | GPT |
|--|------|-----|
| Architecture | Encoder-only | Decoder-only |
| Direction | Bidirectional | Left-to-right (autoregressive) |
| Pre-training | MLM + NSP | Next-token prediction |
| Best for | Understanding / classification | Generation |

## Related

- [[Transformer Architecture]]
- [[Attention Mechanism]]
- [[Model Evaluation Metrics]]
