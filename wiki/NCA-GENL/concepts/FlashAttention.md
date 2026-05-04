---
tags: [concept, attention, optimization, inference, training]
exam: NCA-GENL
domain: Deployment and Optimization
---

# FlashAttention

FlashAttention is a **memory-efficient attention algorithm** that achieves the same mathematical result as standard attention but with dramatically lower GPU memory usage and higher throughput — by restructuring computation to exploit GPU SRAM rather than HBM.

---

## The Problem with Standard Attention

Standard self-attention has two memory bottlenecks:

1. **O(n²) memory:** For a sequence of length n, the full attention matrix is n×n. For n=8192, that's 67M entries — ~256MB in FP16 per head.
2. **Slow HBM access:** Standard attention reads/writes the attention matrix to High Bandwidth Memory (HBM, the main GPU VRAM) multiple times, creating memory bandwidth bottlenecks.

---

## FlashAttention's Solution: Tiled SRAM Computation

**Key insight:** GPU SRAM (L2 cache / shared memory) is much faster than HBM — but tiny (~20MB). FlashAttention breaks the attention matrix computation into **tiles** that fit in SRAM.

### Algorithm Steps

1. Divide Q, K, V matrices into blocks.
2. Load one block of Q, K, V into SRAM.
3. Compute a partial attention result for that tile.
4. Merge partial results using the **online softmax** trick (maintains running max for numerical stability).
5. Never materialize the full n×n attention matrix in HBM.

| Property | Standard Attention | FlashAttention |
|---|---|---|
| Memory complexity | O(n²) | O(n) |
| HBM reads/writes | Many (for full matrix) | Minimal (tiled) |
| Speed | Baseline | 2–4× faster |
| Accuracy | Exact | **Exact** (not approximate) |

---

## Why "Flash"

The name refers to using the GPU's fast SRAM (like flash) instead of slower VRAM/HBM for the inner loop of attention — not to flash memory storage.

---

## Impact

- Enables training and inference on **much longer sequences** (32K, 128K tokens) without OOM.
- Now integrated into PyTorch (`torch.nn.functional.scaled_dot_product_attention`), HuggingFace Transformers, NeMo, and TensorRT-LLM.
- Has become an **industry standard** — most serious LLM training and serving frameworks include it.

---

## FlashAttention vs. Paged Attention

| | FlashAttention | PagedAttention (vLLM) |
|---|---|---|
| **Focus** | Compute efficiency of the attention op | KV cache memory management at serving time |
| **Stage** | Training and single-pass inference | Multi-request batched inference |
| **Memory saving** | Avoids materializing attention matrix | Eliminates KV cache fragmentation |
| **Complementary?** | Yes — TensorRT-LLM uses both |

---

## Exam Notes

- FlashAttention avoids writing the full **O(n²) attention matrix** to HBM.
- Uses **tiled computation in SRAM** — no approximation, mathematically exact.
- Reduces memory and increases speed, especially for **long context** (32K+ tokens).
- Now standard in PyTorch, HuggingFace, NeMo, and TensorRT-LLM.
- Distinct from PagedAttention — they solve different problems and are complementary.

---

## Related

- [[Attention Mechanism]]
- [[vLLM and PagedAttention]]
- [[TensorRT-LLM]]
- [[Quantization]]
- [[Transformer Architecture]]
