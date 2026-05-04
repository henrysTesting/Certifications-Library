---
tags: [concept, inference, llm, optimization, serving]
exam: NCA-GENL
domain: Deployment and Optimization
---

# vLLM and PagedAttention

vLLM is a popular **open-source LLM inference and serving library** optimized for high throughput. Its core innovation is **PagedAttention**, which solves the KV cache memory fragmentation problem using techniques borrowed from OS virtual memory management.

---

## The Problem: KV Cache Fragmentation

During autoregressive LLM inference, each token generated requires attention over all previous tokens. These **key-value pairs are cached** (the KV cache) to avoid recomputation.

**With naive contiguous allocation:**
- Each request's KV cache must be pre-allocated as one contiguous block.
- Memory must be reserved at request start even if the response is short.
- Gaps between allocations create fragmentation — wasted GPU memory.
- Result: Only a fraction of GPU memory is usable, limiting concurrent requests.

---

## PagedAttention

**Insight:** Borrow the OS concept of **virtual memory paging**.

| OS Virtual Memory | PagedAttention |
|---|---|
| Physical memory pages (e.g. 4KB) | KV cache pages (e.g. 16 tokens of KV pairs) |
| Page table maps virtual → physical | Block table maps logical → physical KV slots |
| Demand paging — allocate as needed | Allocate KV cache pages on demand as tokens are generated |
| Pages can be non-contiguous | KV pages can be scattered in GPU memory |

### Benefits
- **Near-zero memory waste:** GPU memory is used at >95% efficiency vs. ~50–60% with contiguous allocation.
- **Flexible batching:** More sequences can run concurrently on the same GPU.
- **Prefix sharing:** Multiple requests sharing a system prompt can share KV cache pages (copy-on-write).

---

## vLLM Architecture

```
Incoming requests → Scheduler → Worker (GPU)
                                  ├── PagedAttention KV cache manager
                                  └── CUDA kernels for token generation
```

- **Continuous batching:** vLLM integrates new requests into the running batch as soon as a slot opens.
- **Multi-GPU support:** Tensor parallelism for serving large models across multiple GPUs.
- **Framework-agnostic:** Supports HuggingFace model weights directly.

---

## vLLM vs. TensorRT-LLM

| Feature | vLLM | TensorRT-LLM |
|---|---|---|
| Origin | Open-source research (UC Berkeley) | NVIDIA-built |
| KV cache | PagedAttention | Paged + integrated with TRT |
| Ease of use | High (load HF weights directly) | Moderate (requires model compilation) |
| Performance | Excellent | Maximum (NVIDIA hardware tuned) |
| Deployment | Standalone or with Triton | Typically with Triton |
| Best for | Fast deployment, flexibility | Maximum throughput on NVIDIA GPUs |

---

## Exam Notes

- vLLM's core innovation is **PagedAttention** — non-contiguous KV cache pages.
- PagedAttention is inspired by **OS virtual memory paging**.
- Solves **KV cache memory fragmentation**, enabling more concurrent requests.
- Also implements **continuous (in-flight) batching** for higher GPU utilization.
- NVIDIA's TensorRT-LLM incorporates similar paged attention concepts.

---

## Related

- [[Attention Mechanism]]
- [[FlashAttention]]
- [[TensorRT-LLM]]
- [[Triton Inference Server]]
- [[Quantization]]
