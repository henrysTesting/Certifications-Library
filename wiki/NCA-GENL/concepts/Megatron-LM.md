---
tags: [concept, nvidia, distributed-training, llm]
exam: NCA-GENL
domain: Deployment and Optimization
---

# Megatron-LM

NVIDIA Megatron-LM is a **pioneering framework for training extremely large Transformer models** — those with hundreds of billions to trillions of parameters — by implementing advanced distributed parallelism techniques.

---

## The Core Problem

A single GPU (even an H100 with 80GB HBM3) cannot hold a 70B+ parameter model in memory. Training requires distributing the model itself across many GPUs, not just the data.

---

## Parallelism Strategies in Megatron-LM

### 1. Tensor Parallelism
- **What:** Splits individual weight matrices across multiple GPUs.
- **How:** For a linear layer `Y = XW`, partition `W` column-wise across GPUs; each GPU computes a partial result, then results are reduced via AllReduce.
- **Granularity:** Within a single transformer layer.
- **Best for:** Very wide layers (large hidden dimensions).

### 2. Pipeline Parallelism
- **What:** Splits the model layer-by-layer across GPUs (GPU 1 handles layers 1–8, GPU 2 handles 9–16, etc.).
- **How:** Uses a pipeline schedule (e.g., GPipe, 1F1B) to pass activations forward and gradients backward.
- **Granularity:** Across transformer blocks.
- **Challenge:** Pipeline bubbles (idle time while waiting for the previous stage).

### 3. Data Parallelism (combined)
- Megatron combines all three: **3D parallelism** = tensor × pipeline × data.
- Enables training of trillion-parameter models across thousands of GPUs.

| Parallelism | Splits | Within/Across | Use case |
|---|---|---|---|
| Data | Batches | Across replicas | Standard multi-GPU |
| Tensor | Weight matrices | Within a layer | Huge layers |
| Pipeline | Model stages (layers) | Across layer groups | Very deep models |

---

## Key Technical Details

- Implements **gradient checkpointing** to trade compute for memory (recompute activations during backward pass).
- Uses **NCCL** for AllReduce communication between GPUs.
- Requires **NVLink/InfiniBand** for low-latency inter-GPU communication at scale.
- Integrated into **NeMo Megatron** for production LLM training.

---

## FasterTransformer (Historical Context)

NVIDIA FasterTransformer was an earlier C++/CUDA library for optimized Transformer inference. Its CUDA kernel optimizations have now been folded into **TensorRT-LLM**, which supersedes it for inference tasks. Megatron-LM remains the standard for training.

---

## Exam Notes

- Megatron-LM solves the problem of **models too large to fit on one GPU**.
- Key techniques: **tensor parallelism** (split weight matrices) + **pipeline parallelism** (split layers).
- Combined with data parallelism = **3D parallelism**.
- Integrated with NeMo as **NeMo Megatron** for enterprise use.
- FasterTransformer → **deprecated**, techniques absorbed into TensorRT-LLM.

---

## Related

- [[NeMo Framework]]
- [[Distributed Deep Learning]]
- [[TensorRT-LLM]]
- [[GPU Architecture and Hardware]]
- [[NVIDIA Compute Systems]]
