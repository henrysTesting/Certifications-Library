# Wiki Index

_Updated: 2026-05-11 | Sources: 3 | Concept pages: 35_

## Exams

| Page | Summary |
|------|---------|
| [[NCA-GENL]] | NVIDIA Certified Associate: Generative AI LLMs — overview and domain map |

## Domains (NCA-GENL)

| Page | Weight | Summary |
|------|--------|---------|
| [[LLM Fundamentals]] | — | Transformers, tokenization, embeddings, backprop, activation functions |
| [[Generative AI Concepts]] | — | Prompt engineering, fine-tuning, RLHF, diffusion models |
| [[NVIDIA AI Stack]] | — | CUDA, RAPIDS, TensorRT, NeMo, Triton, NGC |
| [[Deployment and Optimization]] | — | Quantization, batching, KV cache, distributed training |
| [[RAG and Applications]] | — | RAG pipeline, vector DBs, LangChain, app patterns |

_Note: Exam domain weights (Domain 1–5) are cross-cutting — see [[NCA-GENL]] for the weighted domain map._

## Concepts

| Page | Domain | Summary |
|------|--------|---------|
| [[Transformer Architecture]] | LLM Fundamentals | Full transformer pipeline; encoder/decoder/encoder-decoder types |
| [[Attention Mechanism]] | LLM Fundamentals | Self-attention, multi-head attention, KV cache |
| [[Tokenization]] | LLM Fundamentals | BPE, WordPiece, SentencePiece; subword tokenization |
| [[Embeddings]] | LLM Fundamentals | Dense vector representations; semantic similarity; RAG retrieval |
| [[BERT]] | LLM Fundamentals | Encoder-only; bidirectional; MLM + NSP pretraining |
| [[Activation Functions]] | LLM Fundamentals | ReLU, Sigmoid, Softmax, Tanh; when to use each |
| [[Backpropagation]] | LLM Fundamentals | Forward pass, loss, gradients, hyperparameters, layer norm |
| [[Optimization Algorithms for LLMs]] | LLM Fundamentals | SGD, Momentum, RMSprop, Adam, LARS; adaptive learning rates; when to use each |
| [[RNN]] | LLM Fundamentals | Recurrent networks, LSTM/GRU, sequential processing, temporal dependencies |
| [[Prompt Engineering]] | Generative AI Concepts | Zero/one/few-shot, CoT, temperature, top-p |
| [[Fine-Tuning and LoRA]] | Generative AI Concepts | Full fine-tune, LoRA, QLoRA, knowledge distillation |
| [[Regularization Techniques for LLMs]] | LLM Fundamentals | Dropout, weight decay, early stopping, data augmentation; overfitting prevention |
| [[RLHF]] | Generative AI Concepts | SFT → reward model → PPO; alignment |
| [[Diffusion Models]] | Generative AI Concepts | Forward noise + reverse denoise; image/audio generation |
| [[NVIDIA Ecosystem]] | NVIDIA AI Stack | 6-layer stack; CUDA, RAPIDS, NeMo, memory pooling |
| [[Triton Inference Server]] | Deployment & Optimization | Dynamic batching, concurrent execution, multi-format |
| [[Quantization]] | Deployment & Optimization | FP32→INT8/INT4; PTQ vs QAT; benefits and tradeoffs |
| [[Distributed Deep Learning]] | Deployment & Optimization | Data/model parallelism, AllReduce, NCCL |
| [[RAG]] | RAG & Applications | Full RAG pipeline; chunking; RAG vs. fine-tuning |
| [[Model Evaluation Metrics]] | Experimentation | BLEU, ROUGE, F1, AUC-ROC, benchmarks, A/B testing |
| [[Perplexity and Model Fitting]] | Experimentation | Perplexity as an LLM metric; overfitting vs. underfitting signals |
| [[BERTScore]] | Experimentation | Semantic similarity metric using contextual embeddings; vs. BLEU/ROUGE |
| [[Trustworthy AI]] | Trustworthy AI | Fairness, bias sources, privacy, NeMo Guardrails |
| [[HuggingFace Transformers]] | Software Development | pipeline(), AutoModel, AutoTokenizer, Model Hub |
| [[Python Libraries]] | Software Development | spaCy, LangChain, LangGraph, FAISS, cuDF, ONNX, etc. |
| [[GPU Architecture and Hardware]] | NVIDIA AI Stack | Hopper/Blackwell GPUs, Tensor Cores, Transformer Engine |
| [[NVIDIA Compute Systems]] | NVIDIA AI Stack | DGX/SuperPOD, NVLink/NVSwitch, BlueField DPU, Jetson |
| [[NeMo Framework]] | NVIDIA AI Stack | End-to-end GenAI lifecycle; NeMo Megatron; Guardrails |
| [[Megatron-LM]] | Deployment & Optimization | Tensor + pipeline parallelism for 100B+ model training |
| [[TensorRT-LLM]] | Deployment & Optimization | In-flight batching, paged attention, INT4/FP8 LLM inference |
| [[FlashAttention]] | Deployment & Optimization | Tiled SRAM attention; O(n) memory; exact result |
| [[vLLM and PagedAttention]] | Deployment & Optimization | OS-paged KV cache; high-throughput LLM serving |
| [[NVIDIA Profiling Tools]] | Deployment & Optimization | Nsight, nvidia-smi, DCGM, Fabric Manager |
| [[NVIDIA Platforms and Services]] | NVIDIA AI Stack | AI Enterprise, NGC, DGX Cloud, AI Foundation Models, Riva |
| [[LLM Deployment Strategies]] | Deployment & Optimization | Blue-green, canary, rolling updates; zero-downtime model rollouts |
| [[Feature Engineering]] | Data Analysis | Missing values, encoding, scaling, feature selection, binning; scikit-learn |
| [[Cross-Validation]] | Experimentation | K-fold, stratified k-fold, LOOCV; generalization estimation; overfitting prevention |
| [[Text Embedding Models]] | LLM Fundamentals | Word2Vec, GloVe, FastText, BERT, SBERT, USE; static vs. contextual embeddings |
| [[Model Scalability and Reliability]] | Deployment & Optimization | Latency/throughput, horizontal/vertical scaling, concept drift, data drift, load testing |
| [[Data Privacy and Consent]] | Trustworthy AI | GDPR, CCPA, CIA triad, consent principles, federated learning, differential privacy |
| [[AI Bias Minimization]] | Trustworthy AI | Data/algorithm/interaction bias types, XAI tools (SHAP/LIME), NVIDIA Omniverse Replicator |

## Sources

| Page | Summary |
|------|---------|
| [[GenAINotes]] | Personal study notes — 10 modules + 5-domain exam supplement |
| [[Cheat Sheet for NVIDIA GenAI Ecosystem]] | Hardware + software ecosystem reference; GPU arch, libraries, LLM stack, profiling, services |
| [[NVIDIA-NCA-GENL-Master-Cheat-Sheet]] | Comprehensive NCA-GENL exam prep; all 5 weighted official domains; SkillCertPro |
