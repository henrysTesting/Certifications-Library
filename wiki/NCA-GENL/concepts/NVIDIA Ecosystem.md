---
tags: [concept, nvidia, ecosystem]
exam: NCA-GENL
domain: NVIDIA AI Stack
---

# NVIDIA AI Ecosystem

A 6-layer stack from hardware to software distribution, designed for end-to-end AI workloads.

## The 6 Layers

| Layer | Component | Role |
|-------|-----------|------|
| 1. Hardware Foundation | GPUs, NVIDIA Grace (NVLink) | Raw compute; NVLink connects CPU ↔ GPU efficiently |
| 2. GPU Programming | CUDA | Parallel programming model; CPU organizes, GPU executes |
| 3. Optimization & Acceleration | RAPIDS, TensorRT | Data science on GPU (RAPIDS); model inference optimization (TensorRT) |
| 4. AI Development Framework | NVIDIA NeMo | Full lifecycle: data curation → pretraining → fine-tuning → evaluation |
| 5. Model Deployment | Triton Inference Server | Serve models at scale with dynamic batching and multi-model support |
| 6. Software Distribution | NGC Catalog | Central hub for GPU-optimized containers, models, and software |

## CUDA

- **C**ompute **U**nified **D**evice **A**rchitecture
- Allows leveraging GPU for LLM processing
- Breaks large tasks into smaller identical tasks run in parallel
- Supports C/C++/Python
- GPU as general-purpose accelerator (GPGPU)
- **NVIDIA-SMI**: CLI tool to check GPU stats and verify setup

## RAPIDS

Suite of open-source libraries built on CUDA for GPU-accelerated data science:

| Library | Purpose | Pandas/Sklearn Equivalent |
|---------|---------|--------------------------|
| cuDF | DataFrames | pandas |
| cuML | ML algorithms | scikit-learn |
| cuGraph | Graph analytics | NetworkX |

- Multi-GPU scaling: Dask + RAPIDS
- Multi-node scaling: NCCL + distributed Dask

## Memory Pooling

Pre-allocates and reuses GPU memory instead of allocating/freeing repeatedly.
- Without pooling: 5 steps per allocation (search → reserve → copy → inform GPU → release)
- With pooling: 4 steps once (search → reserve → copy → inform GPU); memory stays reserved

## NeMo

- Modular framework for building, customizing, and deploying Generative AI models
- Built on PyTorch + PyTorch Lightning
- Covers: data curation, pretraining, fine-tuning, evaluation, deployment
- Supports LLMs, speech, and multimodal models
- **NeMo Guardrails**: adds safety rails to LLM applications using Colang declarative rules

## Related

- [[Triton Inference Server]]
- [[Quantization]]
- [[NIM]]
