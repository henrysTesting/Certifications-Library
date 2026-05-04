---
tags: [concept, python, libraries, tooling]
exam: NCA-GENL
domain: Software Development
---

# Python Libraries for AI/ML (Exam Reference)

## Summary Table

| Library | Purpose | Exam Relevance |
|---------|---------|----------------|
| **spaCy** | Industrial NLP: tokenization, NER, POS tagging, dependency parsing | NLP tasks, NER |
| **NumPy** | Numerical computing; array operations | Foundation of all ML pipelines |
| **Keras** | High-level deep learning API on top of TensorFlow | Model building |
| **PyTorch** | Deep learning framework; research-friendly | Training LLMs |
| **TensorFlow** | Deep learning framework; production-friendly | Training and deployment |
| **HuggingFace Transformers** | Pretrained LLMs; `pipeline()` API for quick inference | LLM access |
| **LangChain** | LLM app orchestration: chains, memory, tools, data sources | RAG apps, chatbots |
| **LangGraph** | Stateful, graph-based agent workflows (extends LangChain) | Agentic pipelines |
| **FAISS** | GPU/CPU vector similarity search (Meta) | RAG vector DB |
| **ChromaDB** | Lightweight embedded vector DB | RAG vector DB |
| **Pinecone** | Managed cloud vector DB | RAG vector DB |
| **Weaviate** | Open-source vector DB with filtering | RAG vector DB |
| **cuDF** | GPU-accelerated DataFrames (RAPIDS); mirrors pandas | GPU data processing |
| **cuML** | GPU-accelerated ML algorithms (RAPIDS); mirrors scikit-learn | GPU ML |
| **cuGraph** | GPU-accelerated graph algorithms (RAPIDS) | GPU graph analytics |
| **ONNX** | Open standard for ML model exchange across frameworks | Model portability |

## LangChain Architecture Patterns

- **Chatbot**: `ConversationChain` or `ConversationBufferMemory` — maintains history across turns
- **Summarizer (map-reduce)**: summarize chunks independently → combine summaries
- **Summarizer (refine)**: iteratively update a running summary with each new chunk

## ONNX

Open Neural Network Exchange — open standard for ML models.
- Lets models travel between different frameworks and platforms (PyTorch → TensorRT, etc.)
- Triton Inference Server natively supports ONNX models

## Related

- [[HuggingFace Transformers]]
- [[RAG]]
- [[NVIDIA Ecosystem]]
