---
tags: [concept, scalability, reliability, deployment, mlops]
exam: NCA-GENL
domain: Deployment and Optimization
---

# Model Scalability and Reliability

The capacity to maintain performance under increasing load (scalability) and to serve correct, consistent predictions over time (reliability). Both are required for production LLM deployments.

---

## Scalability Dimensions

### Latency vs. Throughput

| Metric | Definition | Optimization Target |
|--------|-----------|-------------------|
| **Latency** | Time to serve a single request (ms) | Real-time applications; interactive chatbots |
| **Throughput** | Requests (or tokens) served per second | Batch processing; high-concurrency APIs |
| **Time-to-first-token (TTFT)** | Time until first token is generated | Streaming UX; user-perceived responsiveness |

Latency and throughput often trade off — maximizing batch size increases throughput but increases latency per request.

### Horizontal vs. Vertical Scaling

| Strategy | Approach | When to Use |
|----------|---------|------------|
| **Vertical scaling** | Larger/faster hardware (bigger GPU, more VRAM) | Single-node bottleneck; simpler ops |
| **Horizontal scaling** | More instances behind a load balancer | High request volume; fault tolerance |

Horizontal scaling requires stateless inference servers or session-aware routing.

### Scaling Strategies

- **Load balancing** — distribute requests across multiple model replicas
- **Auto-scaling** — spin up/down replicas based on request queue depth or GPU utilization
- **Model replicas** — multiple identical serving instances; enables zero-downtime deployments
- **Caching** — KV cache for attention; prompt caching for repeated prefixes

---

## Reliability in Production

### Concept Drift

The statistical properties of the **input data** change over time, causing model predictions to degrade.

- **Example:** A sentiment model trained on 2020 reviews underperforms on 2024 slang
- **Detection:** Monitor prediction distribution over time; compare to training baseline
- **Response:** Retrain or fine-tune on recent data

### Data Drift

Similar to concept drift but specifically refers to changes in the **feature distribution** (inputs), not necessarily the input-output relationship.

| Drift Type | What Changes | Detection |
|-----------|-------------|----------|
| Concept drift | P(y|x) — the mapping | Monitor output distribution |
| Data drift | P(x) — the input distribution | Monitor input feature statistics |
| Label drift | P(y) — the label distribution | Monitor prediction class balance |

### Load Testing

Before production deployment:
- Simulate expected peak traffic
- Identify latency degradation at scale
- Find memory/OOM thresholds
- Validate auto-scaling response time

**Tools:** Locust, k6, NVIDIA Triton load testing scripts

### Health Monitoring

| Signal | Metric |
|--------|--------|
| GPU utilization | `nvidia-smi`, DCGM |
| Request latency | p50/p95/p99 |
| Error rate | 5xx responses, timeout rate |
| Prediction drift | KL divergence from baseline |
| Memory usage | VRAM headroom, OOM events |

---

## Deployment Patterns for Reliability

See [[LLM Deployment Strategies]] for full coverage of:
- **Blue-green** — zero-downtime switchover
- **Canary** — gradual traffic ramp to new version
- **Rolling update** — replace instances incrementally

---

## Containerization for Scalability

Docker + Kubernetes is the standard for scalable LLM serving:

```
Docker image → pushed to registry
        ↓
Kubernetes Deployment → manages replicas
        ↓
Kubernetes Service → load balances across pods
        ↓
HPA (Horizontal Pod Autoscaler) → scales based on GPU/CPU metrics
```

NVIDIA Triton Inference Server is Kubernetes-native and supports multi-model serving.

---

## Exam Notes

- **Horizontal scaling handles what?** → High request volume and fault tolerance
- **Concept drift vs. data drift:** Concept drift = the model relationship changes; data drift = inputs shift
- **What monitoring detects model degradation in production?** → Output distribution monitoring (concept drift detection)
- **What is the purpose of load testing?** → Validate that the system meets latency/throughput requirements at peak traffic before going live
- **TTFT matters most for:** Interactive streaming chat applications

---

## Related

- [[LLM Deployment Strategies]] — blue-green, canary, rolling deployment patterns
- [[Triton Inference Server]] — production-grade scalable model serving
- [[Quantization]] — reduce model size to serve at scale
- [[vLLM and PagedAttention]] — high-throughput LLM serving
- [[NVIDIA Profiling Tools]] — monitoring GPU utilization in production
