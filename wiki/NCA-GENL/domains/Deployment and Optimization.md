---
tags: [domain, deployment, optimization]
exam: NCA-GENL
sources: 3
---

# Deployment and Optimization

## Core Topics

- **Quantization** — INT8, INT4, FP16, BF16; PTQ vs QAT; tradeoffs between size, speed, accuracy
- **Batching** — static vs dynamic batching; continuous/in-flight batching (Triton)
- **Latency vs throughput** — time-to-first-token (TTFT), tokens-per-second, concurrency
- **KV cache** — cache key-value pairs from attention; avoids recomputation; memory tradeoff
- **Model parallelism** — tensor parallelism, pipeline parallelism for multi-GPU
- **Knowledge distillation** — large teacher → small student model
- **Pruning** — remove weights/neurons that contribute little to output
- **TensorRT** — layer fusion, kernel auto-tuning, FP16/INT8, dynamic batching, QAT
- **Triton Inference Server** — dynamic batching, concurrent execution, multi-format support
- **ONNX** — open standard for model portability across frameworks
- **Distributed training** — data parallelism, model parallelism, AllReduce, NCCL
- **TensorRT-LLM** — LLM-specific inference library; in-flight batching, paged attention, INT4/INT8/FP8
- **In-flight batching** — insert new requests mid-batch as slots free; higher GPU utilization
- **Megatron-LM / 3D parallelism** — tensor + pipeline + data parallelism for 100B+ model training
- **FlashAttention** — tiled SRAM computation eliminates O(n²) HBM writes; exact attention, 2-4× faster
- **PagedAttention / vLLM** — OS-paging-inspired KV cache management; near-zero memory fragmentation
- **CUDA Graph** — record + replay fixed GPU op sequences; eliminates CPU dispatch overhead for decode steps
- **Nsight Systems / Nsight Compute** — system-level vs kernel-level GPU profiling tools
- **nvidia-smi / DCGM** — single-node vs cluster-level GPU monitoring
- **Model scalability** — latency vs. throughput tradeoffs; horizontal vs. vertical scaling; load balancing; auto-scaling replicas
- **Model reliability** — concept drift (P(y|x) changes), data drift (P(x) changes); production monitoring; load testing
- **Containerization** — Docker + Kubernetes for scalable LLM serving; HPA (Horizontal Pod Autoscaler) for GPU-metric-based scaling

## Concept Pages

- [[Quantization]]
- [[Triton Inference Server]]
- [[Distributed Deep Learning]]
- [[NVIDIA Ecosystem]]
- [[TensorRT-LLM]]
- [[Megatron-LM]]
- [[FlashAttention]]
- [[vLLM and PagedAttention]]
- [[NVIDIA Profiling Tools]]
- [[Model Scalability and Reliability]]

## Sources

- [[GenAINotes]] — Module 8 + Domain 3 & 4 supplement
- [[Cheat Sheet for NVIDIA GenAI Ecosystem]] — TensorRT-LLM, Megatron, FlashAttention, vLLM, profiling tools
- [[NVIDIA-NCA-GENL-Master-Cheat-Sheet]] — Domain 3 (Experimentation, 22%); model scalability, latency/throughput, concept drift, data drift, load testing, Docker/Kubernetes
