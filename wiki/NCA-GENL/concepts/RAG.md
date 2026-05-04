---
tags: [concept, rag, retrieval]
exam: NCA-GENL
domain: RAG and Applications
---

# RAG (Retrieval-Augmented Generation)

Combines a retrieval system with an LLM to ground generated answers in external, up-to-date, or private knowledge.

## Problem It Solves

- LLMs have a training cutoff — they don't know recent events
- LLMs have no access to private/enterprise data
- LLMs hallucinate when asked about things not in training data
- RAG injects retrieved facts into the prompt at query time

## How It Works

```
1. INGEST
   Documents → Chunk → Embed each chunk → Store in vector DB

2. QUERY
   User question → Embed query → Similarity search in vector DB
   → Retrieve top-k chunks → Inject into LLM prompt as context
   → LLM generates grounded answer with citations
```

## Key Design Decisions

| Decision | Tradeoff |
|----------|----------|
| Chunk size | Too large = noise in context; too small = missing context |
| Embedding model | Must match at ingest and query time; domain-specific > generic |
| Top-k chunks | More = more context but longer prompt and higher cost |
| Reranking | Cross-encoder reranker re-scores chunks; improves precision at extra compute cost |

## RAG vs. Fine-Tuning

| | RAG | Fine-Tuning |
|--|-----|-------------|
| Knowledge location | Retrieved at query time | Baked into model weights |
| Update cost | Add docs to vector DB | Retrain the model |
| Best for | Dynamic/private data | Specialized behavior/style |

## Vector Databases

Used to store and search embeddings: FAISS, ChromaDB, Pinecone, Weaviate, Milvus, pgvector

## Related

- [[Embeddings]]
- [[Fine-Tuning and LoRA]]
- [[Prompt Engineering]]
- [[Vector Databases]]
