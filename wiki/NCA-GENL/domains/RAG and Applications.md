---
tags: [domain, rag, applications]
exam: NCA-GENL
sources: 1
---

# RAG and Applications

## Core Topics

- **RAG** — ingest (chunk → embed → store) + query (embed → retrieve → inject → generate)
- **Vector databases** — FAISS, ChromaDB, Pinecone, Weaviate; store and search embeddings
- **Chunking strategies** — fixed-size, semantic; chunk size tradeoffs (too large=noise, too small=missing context)
- **Embedding models** — must match at ingest and query time; domain-specific > generic
- **Reranking** — cross-encoder rerankers improve retrieval precision after initial search
- **LangChain / LangGraph** — orchestration frameworks; chatbot memory, summarization patterns, stateful agents
- **RAG vs. Fine-tuning** — RAG = dynamic retrieval, no retraining; Fine-tuning = bake into weights

## Application Patterns

| Pattern | Framework | Notes |
|---------|-----------|-------|
| Chatbot | LangChain ConversationChain | Maintains history; system prompt sets persona |
| Summarizer (map-reduce) | LangChain | Summarize chunks independently → combine |
| Summarizer (refine) | LangChain | Iteratively update running summary per chunk |
| Stateful agent | LangGraph | Graph-based; handles multi-step tool use |

## Concept Pages

- [[RAG]]
- [[Embeddings]]
- [[Python Libraries]]

## Sources

- [[GenAINotes]] — Module 6 + Domain 1 & 4 supplement
