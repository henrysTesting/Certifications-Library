---
tags: [concept, deployment, inference, optimization]
exam: NCA-GENL
domain: Deployment and Optimization
---

# LLM Deployment Strategies

Strategies for updating and serving large language models in production with minimal or zero downtime.

---

## Zero-Downtime Update Strategies

| Strategy | How It Works | Downtime | Rollback | Best For |
|---|---|---|---|---|
| **Blue-Green** | Two identical environments (blue=live, green=new); switch traffic instantly | Zero (instantaneous) | Instant (flip back to blue) | Large-scale LLM updates needing full validation |
| **Canary** | Gradual rollout to a subset of users; monitor → expand → full | Zero (staged) | Partial (revert subset) | Risk mitigation; catching issues before full exposure |
| **Rolling** | Update instances in phases; old and new versions overlap briefly | Near-zero | Complex (mixed versions) | Resource-constrained environments; Kubernetes clusters |
| **Hotfix** | Skip full testing; deploy immediately | Varies | Difficult | Emergency only — **not a best practice** |

---

## Blue-Green Deployment

The primary strategy for zero-downtime LLM updates at scale.

```
Traffic → Load Balancer → [Blue: current model] (live)
                        → [Green: new model]   (idle, warming up)

After validation:
Traffic → Load Balancer → [Green: new model]   (live)
                        → [Blue: old model]    (standby for rollback)
```

**Steps:**
1. Deploy new model version to idle (green) environment
2. Warm up green fully — run validation, check latency/accuracy
3. Switch load balancer to send all traffic to green
4. Keep blue on standby for instant rollback if needed

**Advantages for LLMs:**
- No user request ever hits an unvalidated model
- Rollback is instantaneous — flip traffic back to blue
- Full environment parity — green mirrors blue exactly before cutover

---

## Canary Deployment

Gradual traffic shifting to detect issues before full rollout.

```
95% traffic → Old model
 5% traffic → New model (canary)
     ↓ monitor metrics
25% traffic → New model
     ↓ monitor metrics
100% traffic → New model
```

**When to use:**
- LLM behavioral changes that are hard to catch in testing (hallucination rates, tone, output format)
- Large user base where even a small failure rate is significant
- A/B testing new fine-tuned versions against baseline

**Used alongside blue-green:** Many enterprises run canary *within* a blue-green setup — switch green live, then gradually ramp traffic from 5% → 100%.

---

## Rolling Updates

Update model serving instances one at a time or in batches.

- Native to Kubernetes — update pods incrementally
- Old and new versions briefly serve traffic simultaneously
- Lower infrastructure cost than blue-green (no duplicate full environment)

**Limitation for LLMs:** If old and new model behave differently, users may get inconsistent responses during the rollout window.

---

## Model Versioning with Triton

[[Triton Inference Server]] supports native model versioning:

- Multiple versions of the same model loaded simultaneously
- Traffic routing rules define which version handles requests
- Supports controlled rollouts and instant rollback if a version misbehaves

**Integration pattern:**
```
Triton Inference Server
├── model/
│   ├── 1/  ← old version (standby)
│   └── 2/  ← new version (active)
```

---

## Exam Notes

- **Blue-green** = two full environments; instantaneous traffic switch; best for zero-downtime with full rollback capability
- **Canary** = gradual rollout to a subset; best for catching behavioral issues before full exposure
- **Rolling** = phased instance updates; best for Kubernetes/resource-constrained deployments
- **Hotfix without testing** = not a best practice; avoid in exam answers
- [[Triton Inference Server]] natively supports model versioning for controlled rollouts
- For "zero downtime" + "full rollback," **blue-green is the canonical answer**

---

## Related

- [[Triton Inference Server]]
- [[TensorRT-LLM]]
- [[Distributed Deep Learning]]
- [[Model Evaluation Metrics]]
- [[Trustworthy AI]]
