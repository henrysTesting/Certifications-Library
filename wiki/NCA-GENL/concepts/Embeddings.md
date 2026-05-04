---
tags: [concept, embeddings, nlp]
exam: NCA-GENL
domain: LLM Fundamentals
---

# Embeddings

Dense vector representations that capture the semantic meaning of tokens, words, or sentences. Words/sentences close in meaning are close in vector space.

## Types

| Type | Description |
|------|-------------|
| Word embeddings | Vector per word; classic models: Word2Vec, GloVe |
| Token embeddings | Vector per token (subword); used inside transformers |
| Sentence / text embeddings | Single vector for a whole sentence; used in RAG retrieval |
| Positional encodings | Added to token embeddings to encode word order |

## Why Embeddings Matter

- Converts text (discrete symbols) into continuous numeric space where math works
- Semantic similarity = cosine similarity between vectors (0 = unrelated, 1 = identical)
- Foundation for semantic search, RAG, and classification

## In the Transformer Pipeline

`Token IDs → Embedding layer → Dense vectors → + Positional encoding → Self-attention`

## Embedding Models for RAG

- Must use the **same embedding model** at both ingest time and query time
- Popular: BERT-based sentence transformers, NVIDIA NV-Embed
- Domain-specific embedding models outperform generic ones for specialized corpora

## Exam Note

- Word embeddings predate transformers (Word2Vec → LLM evolution path per notes)
- Embedding classifiers: first convert input to vector, then classify — captures meaning, not just exact words

## Related

- [[Tokenization]]
- [[Transformer Architecture]]
- [[RAG]]
