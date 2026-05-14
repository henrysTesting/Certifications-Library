---
tags: [concept, training, optimization, algorithms]
exam: NCA-GENL
domain: LLM Fundamentals
sources: 0
---

# Optimization Algorithms for LLMs

## Overview

Optimization algorithms adjust model weights during training to minimize loss. Different optimizers have different strategies for setting learning rates and handling gradient variance, making them suitable for different training scenarios.

For large language models, the choice of optimizer significantly impacts training stability, convergence speed, and final model quality.

## Core Optimizers

### Stochastic Gradient Descent (SGD)

The simplest optimization method: update weights in the direction opposite to the gradient.

**Update rule:**
```
w = w - learning_rate × gradient
```

**Characteristics:**
- Single learning rate for all parameters
- No adaptation based on gradient history
- Fast and memory-efficient
- Can get stuck in local minima or plateau on non-stationary objectives

**When to use:**
- Baseline comparisons
- When computational resources are extremely limited
- Simple problems with stable gradients

**Exam tip:** SGD is the baseline — don't use it for LLMs in production.

### Momentum

Adds a velocity term to SGD: accumulate gradients over time to "build momentum" down the loss landscape.

**Update rule:**
```
velocity = β × velocity + gradient
w = w - learning_rate × velocity
```

**Characteristics:**
- Accelerates convergence in consistent gradient directions
- Helps escape shallow local minima
- Reduces oscillation
- Typical β = 0.9

**Benefits:**
- Faster convergence than vanilla SGD
- Better stability on non-convex objectives

**Limitations:**
- Still uses a single, fixed learning rate
- Doesn't adapt to gradient variance

**When to use:**
- When SGD training is slow or oscillatory
- As a building block for more advanced methods (Adam, RMSprop use momentum variants)

### RMSprop (Root Mean Square Propagation)

Dynamically adjusts the learning rate based on the magnitude of recent gradients.

**Key insight:** Divide the learning rate by the root-mean-square of recent gradients.

**Update rule:**
```
squared_grad_accumulation = β × squared_grad_accumulation + (1-β) × gradient²
adaptive_learning_rate = learning_rate / (sqrt(squared_grad_accumulation) + ε)
w = w - adaptive_learning_rate × gradient
```

**Characteristics:**
- **Adaptive:** Learning rate scales inversely with gradient magnitude
- Large gradients → smaller updates (prevents divergence)
- Small gradients → larger updates (accelerates learning)
- Typically β = 0.9, ε = 1e-8

**Advantages:**
- **Most effective for LLM training:** Handles non-stationary objectives well
- Robust to learning rate choice
- Lower memory overhead than Adam
- Good for sparse gradients

**Limitations:**
- Less commonly used than Adam (Adam is more "universal")
- Slightly slower than Adam in some scenarios

**Exam relevance:** RMSprop is specifically highlighted for LLM training because it handles gradient variance effectively without the overhead of methods like Adam.

### Adam (Adaptive Moment Estimation)

Combines momentum and RMSprop: maintains both first-moment (mean) and second-moment (variance) estimates.

**Update rule:**
```
m = β₁ × m + (1-β₁) × gradient        # First moment (mean)
v = β₂ × v + (1-β₂) × gradient²       # Second moment (variance)
m_hat = m / (1 - β₁ᵗ)                  # Bias correction
v_hat = v / (1 - β₂ᵗ)                  # Bias correction
w = w - learning_rate × m_hat / (sqrt(v_hat) + ε)
```

**Characteristics:**
- Typically β₁ = 0.9, β₂ = 0.999, ε = 1e-8
- Combines momentum (β₁) with adaptive scaling (β₂)
- Bias correction for early training steps

**Advantages:**
- Very robust across different problem types
- Works well "out of the box" with default hyperparameters
- Widely adopted and well-understood
- Good convergence speed

**Limitations:**
- Slightly higher memory overhead than RMSprop (stores two moment estimates)
- Can over-adapt and converge to suboptimal solutions in some cases
- Not specifically optimized for LLM training

**When to use:**
- When you need a safe default choice
- For diverse problems where no specific optimizer is preferred
- When computational resources allow the extra memory

### Layer-wise Adaptive Rate Scaling (LARS)

Scales learning rates on a per-layer basis based on the ratio of weight norm to gradient norm.

**Key insight:** Different layers of large models have very different gradient magnitudes; adapt learning rates accordingly.

**Update rule:**
```
local_lr = learning_rate × ||weights|| / (||gradients|| + weight_decay_coeff)
w = w - local_lr × gradient
```

**Characteristics:**
- Layer-wise adaptation
- Particularly useful for distributed training
- Enables larger batch sizes without divergence
- Typically used with momentum or weight decay

**Advantages:**
- Enables large-batch training (useful for distributed LLM training)
- Reduces training time with more GPUs
- Stable across different layer depths

**Limitations:**
- More complex to implement than Adam/RMSprop
- Introduces additional hyperparameter tuning
- Primarily designed for large-scale distributed training

**When to use:**
- Distributed training of very large models
- When trying to maximize throughput with large batch sizes
- LLM training at scale (100B+ parameters)

## Comparison Matrix

| Optimizer | Adaptive LR | Momentum | Memory | Speed | LLM-Suitable | Exam Highlight |
|-----------|------------|----------|--------|-------|--------------|-----------------|
| **SGD** | ❌ | ❌ | ✅ (minimal) | ✅ (baseline) | ❌ | Baseline only |
| **SGD + Momentum** | ❌ | ✅ | ✅ | ✅ | ⚠️ | Better than SGD |
| **RMSprop** | ✅ | ❌ | ✅ | ✅ | ✅ | **Best for LLM variance handling** |
| **Adam** | ✅ | ✅ | ⚠️ (higher) | ✅ | ✅ | Universal default |
| **LARS** | ✅ (per-layer) | ✅ | ⚠️ | ✅ | ✅ | Distributed training at scale |

## Common Exam Patterns

| Question Pattern | Answer |
|------------------|--------|
| "Which optimizer dynamically adjusts learning rate based on gradient variance?" | **RMSprop** or **Adam** (RMSprop more direct) |
| "Which optimizer is best for non-stationary objectives in LLM training?" | **RMSprop** |
| "Which optimizer combines momentum with adaptive learning rates?" | **Adam** |
| "Which optimizer enables large-batch distributed training?" | **LARS** |
| "Which optimizer has the lowest memory overhead?" | **RMSprop** or **SGD** |
| "Which optimizer works best 'out of the box'?" | **Adam** |
| "Most effective for LLMs: adjusts learning rate based on gradient variance" | **RMSprop** |

### Tricky Distinctions

| Misconception | Truth |
|---------------|-------|
| "Adam is always better than RMSprop" | False — RMSprop is more efficient for LLMs; Adam is a safer default for unknown problems |
| "Momentum prevents overfitting" | False — Momentum accelerates training but doesn't prevent overfitting; use regularization instead |
| "LARS is required for distributed training" | False — You can use Adam/RMSprop + data parallelism; LARS enables *larger batch sizes* |
| "SGD is obsolete" | False — SGD + momentum is still used; not ideal for LLMs but valid for comparison |
| "RMSprop is only for sparse gradients" | False — It works for dense gradients too; it's general-purpose adaptive |

## Choosing an Optimizer for Your LLM

| Scenario | Recommended Optimizer | Reasoning |
|----------|----------------------|-----------|
| Single-GPU fine-tuning | Adam or RMSprop | Stable, good defaults; RMSprop slightly more efficient |
| Large batch training (100K+) | LARS | Enables large batches without divergence |
| Pre-training from scratch | RMSprop or LARS | Handles non-stationary loss landscape; gradient variance is critical |
| Transfer learning / LoRA | Adam | Safe default; fine-tuning is stable |
| Sparse gradient problems | RMSprop | Designed for sparse updates |
| Unknown/diverse problems | Adam | Most robust "out of the box" |

## Related

- [[Backpropagation]]
- [[Regularization Techniques for LLMs]]
- [[Distributed Deep Learning]]
- [[Fine-Tuning and LoRA]]
