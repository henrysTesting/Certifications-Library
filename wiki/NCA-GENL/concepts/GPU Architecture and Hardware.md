---
tags: [concept, nvidia, hardware, gpu]
exam: NCA-GENL
domain: NVIDIA AI Stack
---

# GPU Architecture and Hardware

NVIDIA's AI hardware stack spans GPU microarchitecture, specialized compute units, and the intelligent firmware that ties them together.

---

## GPU Architectures

| Architecture | Products | Key Role |
|---|---|---|
| **Hopper** | H100, H200 | Current flagship; market leader for AI training & inference |
| **Blackwell** | B100, B200, GB200 | Next-gen; system-level innovations targeting trillion-parameter models |

- **Hopper** introduced the Transformer Engine (FP8 precision), NVLink 4.0, and HBM3 memory.
- **Blackwell** pushes further with higher memory bandwidth and multi-chip module (MCM) design in GB200.
- Both serve as the compute foundation for data center AI, powering DGX systems.

---

## Tensor Cores

Tensor Cores are **specialized matrix multiply-accumulate (MMA) hardware units** inside NVIDIA GPUs.

- **Purpose:** Dramatically accelerate the D = A × B + C operation that dominates deep learning.
- **Why they matter:** Transformer attention, linear projections, and convolutions are all dense matrix multiplications — Tensor Cores handle these in a single clock cycle at massive throughput.
- **Precision support:** FP64, TF32, FP16, BF16, FP8, INT8, INT4 (varies by generation).
- **Throughput advantage:** Orders of magnitude faster than CUDA Cores for matrix ops.

| Generation | Precision Added | Notable Feature |
|---|---|---|
| Volta (V100) | FP16 | First Tensor Core generation |
| Ampere (A100) | BF16, TF32 | Sparsity acceleration (2× for 50% sparse weights) |
| Hopper (H100) | FP8 | Transformer Engine integration |
| Blackwell | FP4 | 4-bit compute for ultra-dense inference |

---

## Transformer Engine

The **Transformer Engine** is a hardware + software co-design feature introduced in Hopper (H100).

- **Problem it solves:** Transformer models need both precision (for accuracy) and speed (for training throughput) — fixed-precision training forces a compromise.
- **Solution:** Dynamically switches between **FP8** and **FP16** precision on a per-layer, per-tensor basis.
  - FP8 = faster computation, smaller memory footprint.
  - FP16 = higher precision where needed (e.g., attention softmax, layer norm).
- **Result:** Significant speedup over pure FP16 training with no accuracy loss.
- **Integration:** Exposed through cuDNN, and natively supported in PyTorch and NeMo.

---

## Exam Notes

- Know Hopper = H100/H200; Blackwell = B100/B200/GB200.
- Tensor Cores accelerate **matrix multiply-accumulate** — the core operation of all Transformer layers.
- Transformer Engine is specific to **Hopper and newer** — it dynamically switches FP8 ↔ FP16.
- FP8 training requires the Transformer Engine; not available on older architectures.

---

## Related

- [[NVIDIA Ecosystem]]
- [[NVIDIA Compute Systems]]
- [[Quantization]]
- [[TensorRT-LLM]]
- [[Distributed Deep Learning]]
