---
tags: [domain, nvidia, tooling]
exam: NCA-GENL
sources: 2
---

# NVIDIA AI Stack

## The 6-Layer Stack

| Layer | Component |
|-------|-----------|
| Hardware Foundation | GPUs, NVIDIA Grace, NVLink |
| GPU Programming | CUDA, NVIDIA-SMI |
| Optimization & Acceleration | RAPIDS (cuDF, cuML, cuGraph), TensorRT |
| AI Development Framework | NeMo (+ NeMo Guardrails) |
| Model Deployment | Triton Inference Server (NVIDIA Dynamo Triton) |
| Software Distribution | NGC Catalog |

## Core Topics

- **CUDA** — parallel programming; CPU organizes, GPU executes; thousands of cores in parallel
- **RAPIDS** — GPU-accelerated data science suite; mirrors pandas/scikit-learn/NetworkX APIs
- **TensorRT** — inference optimizer: layer fusion, kernel auto-tuning, dynamic batching, FP16/INT8
- **NeMo** — full lifecycle LLM framework (pretraining → fine-tuning → evaluation → deployment)
- **NeMo Guardrails** — safety rails defined in Colang; prevents harmful/off-topic outputs
- **Triton** — multi-format model server with dynamic batching and concurrent execution
- **NGC Catalog** — central hub for GPU-optimized containers and models
- **Memory pooling** — pre-allocate GPU memory; reduces per-transfer overhead
- **Tensor Cores** — specialized MMA units in GPU; accelerate matrix multiply-accumulate ops critical for Transformers
- **Transformer Engine** — Hopper+ feature; dynamically switches FP8 ↔ FP16 for speed without accuracy loss
- **Hopper / Blackwell** — current/next-gen NVIDIA GPU architectures; H100/H200 vs B100/B200/GB200
- **DGX / SuperPOD** — all-in-one AI server / cluster blueprint for enterprise LLM training
- **NVLink / NVSwitch** — high-speed GPU interconnect; NVSwitch enables full-mesh any-to-any GPU comms
- **BlueField DPU** — offloads networking/storage from GPU; keeps GPUs 100% on AI compute
- **NeMo Framework** — end-to-end GenAI lifecycle: data → pretrain → fine-tune → deploy
- **NeMo Megatron** — NeMo + Megatron-LM integration; flagship solution for 100B+ parameter training
- **NVIDIA Riva** — GPU-accelerated conversational AI SDK; ASR + NLP + TTS
- **NVIDIA AI Enterprise** — enterprise-certified NVIDIA software bundle with support and stability guarantees
- **DGX Cloud** — rent DGX-class compute from CSPs (Azure, GCP, Oracle)

## Concept Pages

- [[NVIDIA Ecosystem]]
- [[Triton Inference Server]]
- [[Quantization]]
- [[GPU Architecture and Hardware]]
- [[NVIDIA Compute Systems]]
- [[NeMo Framework]]
- [[NVIDIA Platforms and Services]]

## Sources

- [[GenAINotes]] — Module 8 + Domain 4 supplement
- [[Cheat Sheet for NVIDIA GenAI Ecosystem]] — full NVIDIA hardware + software ecosystem reference
