---
tags: [concept, embeddings, nlp, text-embedding]
exam: NCA-GENL
domain: LLM Fundamentals
---

# Text Embedding Models

Models that convert text (words, sentences, documents) into dense numerical vectors that encode semantic meaning. The embedding space places semantically similar items close together.

---

## Why Text Embeddings?

Raw text is discrete and high-dimensional. Embeddings give models a continuous, dense, and learnable representation of language. They are the foundation of semantic search, RAG retrieval, clustering, and classification.

---

## Word-Level Embedding Models

### Word2Vec (Google, 2013)

Two architectures, both trained via self-supervised prediction:

| Architecture | Predicts | Speed | Context |
|-------------|---------|-------|---------|
| CBOW (Continuous Bag of Words) | Center word from context | Faster | Better frequent words |
| Skip-gram | Context words from center | Slower, better | Better rare words |

**Key property:** Captures analogies — `king − man + woman ≈ queen`
**Limitation:** Static — one vector per word regardless of context

### GloVe (Stanford, 2014)

- Trains on **global word co-occurrence statistics** across corpus
- Combines benefits of matrix factorization and local context window
- Static embeddings like Word2Vec

**GloVe vs. Word2Vec:**
- GloVe uses global statistics; Word2Vec uses local windows
- GloVe is often better on word analogy tasks
- Both produce static embeddings

### FastText (Facebook, 2016)

- Extends Word2Vec by representing words as **bags of character n-grams**
- `"playing"` → `{pla, lay, ayi, yin, ing, <pl, ng>}` + the full word
- Can generate embeddings for **out-of-vocabulary (OOV) words**
- Better for morphologically rich languages and misspellings

---

## Sentence / Document Embedding Models

### BERT (Google, 2018)

- **Contextual** embeddings — the same word gets different vectors in different sentences
- Trained with Masked Language Model (MLM) + Next Sentence Prediction (NSP)
- Each token's embedding encodes its full bidirectional context

**Limitation for sentence embeddings:** Raw `[CLS]` token representation is suboptimal for sentence similarity

See [[BERT]] for full architecture details.

### Sentence-BERT (SBERT)

- Fine-tuned BERT using **siamese network** structure on sentence pairs
- Optimized specifically for **semantic textual similarity**
- Can compare sentence embeddings with cosine similarity efficiently
- **Use case:** Semantic search, RAG retrieval, duplicate detection, clustering

**SBERT vs. BERT for similarity:**
- BERT requires passing both sentences together (O(n²) for n sentences)
- SBERT embeds each sentence independently — much faster

### Universal Sentence Encoder (USE)

- Google model; two variants: Transformer (higher accuracy) and DAN (faster)
- Produces fixed-length 512-dim sentence embeddings
- Good for short semantic similarity tasks

### OpenAI Embeddings (text-embedding-ada-002 / text-embedding-3)

- API-based; produces 1536-dim or configurable-dim embeddings
- Strong general-purpose performance on diverse retrieval tasks
- Used widely in RAG pipelines

---

## Comparison Matrix

| Model | Contextual | OOV Handling | Speed | Best Use Case |
|-------|-----------|-------------|-------|---------------|
| Word2Vec | No (static) | No | Fast | Word analogies, simple NLP |
| GloVe | No (static) | No | Fast | Word similarity; global co-occurrence |
| FastText | No (static) | Yes (n-grams) | Fast | Noisy text, morphological languages |
| BERT | Yes | No | Slow | Token-level tasks (NER, QA) |
| SBERT | Yes | No | Moderate | Sentence similarity, RAG retrieval |
| USE | Yes | No | Fast | Short text similarity |
| OpenAI Embeddings | Yes | No | API latency | General RAG, production search |

---

## Embedding Models in RAG

RAG retrieval requires:
1. **Ingest time:** Embed document chunks → store in vector DB
2. **Query time:** Embed user query → similarity search

**Critical rule:** The same embedding model must be used at ingest AND query time. Switching models invalidates the index.

---

## Exam Notes

- **Which embedding handles out-of-vocabulary words?** → FastText (n-gram subwords)
- **Which model is specifically optimized for sentence similarity?** → SBERT (Sentence-BERT)
- **Word2Vec CBOW vs. Skip-gram:** CBOW predicts center from context; Skip-gram predicts context from center
- **Static vs. contextual:** Word2Vec/GloVe/FastText are static; BERT/SBERT/USE are contextual
- **When to use contextual embeddings:** When word meaning depends on surrounding context (polysemy)

---

## Related

- [[Embeddings]] — general embedding concepts, dense vector representations
- [[BERT]] — full BERT architecture and pretraining
- [[RAG]] — text embedding models in retrieval pipelines
- [[Feature Engineering]] — embeddings as features for downstream models
- [[BERTScore]] — uses contextual BERT embeddings for evaluation
