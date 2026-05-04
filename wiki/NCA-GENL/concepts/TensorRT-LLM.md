---
tags: [concept, nvidia, inference, llm, optimization]
exam: NCA-GENL
domain: Deployment and Optimization
---

# TensorRT-LLM

NVIDIA TensorRT-LLM is an **open-source library for accelerating and optimizing LLM inference**, built on top of TensorRT. It is NVIDIA's primary recommended solution for production LLM serving today.

---

## Relationship to TensorRT

| | TensorRT | TensorRT-LLM |
|---|---|---|
| **Target** | General deep learning models | Large language models specifically |
| **Key techniques** | Layer fusion, kernel auto-tuning, precision quantization | All of TensorRT + in-flight batching, paged attention, speculative decoding |
| **Interface** | C++/Python SDK | Python library with pre-built LLM kernels |
| **Status** | General purpose | LLM-optimized |

TensorRT-LLM wraps TensorRT and adds LLM-specific optimizations on top.

---

## Core Techniques

### In-Flight Batching (Continuous Batching)
- **Problem:** Static batching makes fast-finishing requests wait for slow ones.
- **Solution:** New requests are inserted into the batch the moment a slot frees up, without waiting for the entire batch to complete.
- **Result:** Higher GPU utilization and throughput.

### Paged Attention
- Borrowed from vLLM's PagedAttention concept.
- **Problem:** KV cache for each sequence is allocated contiguously; memory fragmentation wastes GPU memory.
- **Solution:** Break KV cache into fixed-size pages (like OS virtual memory); allocate non-contiguously.
- **Result:** More sequences can run concurrently, reducing memory waste.

### Quantization Support
- Supports **INT4, INT8, FP8** quantization.
- FP8 requires Hopper (H100) or newer hardware (Transformer Engine).
- Reduces memory footprint and increases throughput with minimal accuracy loss.

### CUDA Graph Integration
- **CUDA Graph** records a sequence of GPU operations as a replayable graph.
- For LLM decode steps (which have a fixed computation pattern), replaying the graph eliminates CPU dispatch overhead.
- Reduces per-token latency in autoregressive generation.

### Kernel Fusion
- Fuses multiple sequential operations (e.g., attention + softmax + dropout) into a single GPU kernel.
- Reduces memory round-trips and kernel launch overhead.

---

## Deployment with Triton

TensorRT-LLM is typically deployed **behind Triton Inference Server**:
- TensorRT-LLM handles model compilation and optimized execution.
- Triton handles request routing, batching orchestration, and the serving API.

---

## Exam Notes

- TensorRT-LLM is the **current primary NVIDIA inference library for LLMs** (replacing FasterTransformer).
- Key features: **in-flight batching**, **paged attention**, **INT4/INT8/FP8 quantization**, **CUDA Graph**.
- In-flight batching = continuous batching = insert new requests into running batch immediately.
- FP8 quantization requires **Hopper (H100) or newer**.
- Integrates with Triton Inference Server for production deployment.

---

## Related

- [[Triton Inference Server]]
- [[Quantization]]
- [[Attention Mechanism]]
- [[vLLM and PagedAttention]]
- [[GPU Architecture and Hardware]]
- [[NeMo Framework]]
