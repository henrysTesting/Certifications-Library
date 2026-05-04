---
tags: [concept, distributed, training, deployment]
exam: NCA-GENL
domain: Deployment and Optimization
---

# Distributed Deep Learning

Training and serving very large models across multiple GPUs and nodes.

## Why It's Needed

- Modern LLMs have billions of parameters that don't fit in a single GPU's VRAM
- Training at scale requires parallelizing compute across many GPUs

## Parallelism Strategies

| Strategy | How | When |
|----------|-----|------|
| **Data parallelism** | Same model copied to each GPU; each processes a different data batch; gradients averaged | Model fits in one GPU; need to scale throughput |
| **Model parallelism** | Model layers split across GPUs | Model too large for one GPU |
| **Tensor parallelism** | Individual weight matrices split across GPUs | Very large layers within a model |
| **Pipeline parallelism** | Groups of layers on different GPUs; data flows in pipeline stages | Deep models distributed across many GPUs |

## AllReduce

Communication pattern to average gradients across all GPUs after each backward pass.

- **Ring-AllReduce**: each GPU sends/receives from neighbors in a ring; efficient bandwidth use
- Every GPU ends up with the same averaged gradients → synchronized weight updates

## NCCL (NVIDIA Collective Communications Library)

NVIDIA's optimized library for multi-GPU and multi-node communication.
- Used under the hood by PyTorch, TensorFlow, and NeMo for distributed training
- Implements AllReduce, broadcast, reduce, gather operations

## Scalability in Production

| Goal | Approach |
|------|----------|
| High throughput | Dynamic batching (Triton), horizontal scaling |
| Low latency | Quantization, TensorRT, smaller models |
| Fault tolerance | Redundancy, checkpointing |
| Scalability | Load balancing across model replicas |

## Related

- [[NVIDIA Ecosystem]]
- [[Triton Inference Server]]
- [[Quantization]]
