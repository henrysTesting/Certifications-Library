---
tags: [source, nvidia, ecosystem, hardware, deployment]
exam: NCA-GENL
domain: NVIDIA AI Stack
ingested: 2026-04-24
---

# Cheat Sheet for NVIDIA GenAI Ecosystem

**Author:** DolbyUUU (https://github.com/DolbyUUU)
**Source:** `raw/NCA-GENL/Cheat Sheet for NVIDIA GenAI Ecosystem.pdf`
**Scope:** A reference covering the full NVIDIA GenAI hardware and software ecosystem — from GPU silicon to cloud services.

---

## Section Coverage

| Section | Topics Covered |
|---------|---------------|
| GPU Architecture & Cores | Hopper/Blackwell architectures, Tensor Cores, Transformer Engine |
| Compute & Networking Systems | DGX/SuperPOD, NVLink/NVSwitch, BlueField DPU, Spectrum-X, Jetson |
| Core Platforms & Libraries | CUDA, CUDA-X AI (cuDNN, NCCL, DALI), RAPIDS (cuDF, cuML), cuBLAS/cuSPARSE |
| LLM/GenAI-Specific Software Stack | NeMo, Megatron-LM, NeMo Megatron, FasterTransformer, TensorRT-LLM, CUDA Graph, NeMo Guardrails |
| Inference & Deployment | TensorRT, Triton Inference Server |
| Dev, Profiling & Management Tools | Nsight Suite, nvidia-smi, DCGM, Fabric Manager, Base Command Manager |
| Platforms, Applications & Services | AI Enterprise, NGC Catalog, DGX Cloud, AI Foundation Models, Riva |
| Ecosystem Partners & Open Source | PyTorch, TensorFlow/JAX, FlashAttention, vLLM, Kubernetes, InfiniBand |

---

## Key Concepts Extracted

### Hardware
- [[GPU Architecture and Hardware]] — Hopper (H100/H200), Blackwell (B100/B200/GB200), Tensor Cores, Transformer Engine
- [[NVIDIA Compute Systems]] — DGX/SuperPOD, NVLink/NVSwitch, BlueField DPU, Spectrum-X, Jetson AGX

### Core Libraries
- [[NVIDIA Ecosystem]] — CUDA, CUDA-X AI, cuDNN, NCCL, DALI, RAPIDS, cuDF, cuML, cuBLAS/cuSPARSE *(existing — enriched)*

### LLM Software Stack
- [[NeMo Framework]] — End-to-end GenAI training/deployment; NeMo Megatron integration
- [[Megatron-LM]] — Tensor & pipeline parallelism for 100B+ parameter model training
- [[TensorRT-LLM]] — In-flight batching, paged attention, INT4/INT8 for LLM inference
- [[Trustworthy AI]] — NeMo Guardrails *(existing — enriched)*

### Inference Optimization
- [[FlashAttention]] — Memory-efficient attention via tiled SRAM computation
- [[vLLM and PagedAttention]] — KV cache paging for high-throughput LLM serving

### Profiling & Management
- [[NVIDIA Profiling Tools]] — Nsight Systems, Nsight Compute, nvidia-smi, DCGM, Fabric Manager

### Platforms & Services
- [[NVIDIA Platforms and Services]] — AI Enterprise, NGC Catalog, DGX Cloud, AI Foundation Models, Riva

### Ecosystem / Open Source
- [[Distributed Deep Learning]] — NCCL, InfiniBand, Kubernetes + GPU Operator *(existing — enriched)*
