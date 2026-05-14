---
tags: [concept, evaluation, metrics]
exam: NCA-GENL
domain: Experimentation
---

# Perplexity and Model Fitting

## What Is Perplexity?

Perplexity measures how well a language model predicts a test dataset — specifically, the inverse probability of the test set normalized by the number of tokens:

$$\text{Perplexity} = e^{-\frac{1}{N}\sum \log P(x)}$$

- **Lower perplexity** = model assigns higher probability to actual sequences = better fit
- **Higher perplexity** = model assigns lower probability to actual sequences = poorer fit

## Perplexity and Overfitting / Underfitting

| Scenario | Perplexity | What It Means |
|----------|-----------|---------------|
| Underfitting (model too simple) | High | Cannot capture patterns; high loss on both train and test |
| Optimal fit | Moderate | Balanced bias and variance |
| Overfitting (model memorizes training data) | Very low on train, higher on test | Fails to generalize to held-out data |

### Key Rule

A lower perplexity **does not always mean better**. Very low perplexity on training data paired with higher perplexity on test data signals overfitting.

To properly diagnose model fit, always compare **training perplexity vs. test perplexity**:

| Gap | Interpretation |
|-----|---------------|
| Both high | Underfitting |
| Large gap (train low, test high) | Overfitting |
| Small gap, both moderate | Good generalization |

## Common Exam Traps

| Statement | Verdict |
|-----------|---------|
| "Lower perplexity always means more accurate and no overfit/underfit" | **False** — low perplexity can indicate overfitting |
| "Optimal perplexity ensures no overfit/underfit regardless of complexity" | **False** — complexity still matters; must compare train vs. test |
| "Balancing complexity and diversity guarantees optimal perplexity regardless of training time" | **False** — training time (epochs) directly affects overfitting risk |
| "Higher perplexity → underfitting; too low → possible overfitting" | **Correct** |

## Related

- [[Model Evaluation Metrics]]
- [[Backpropagation]]
- [[Fine-Tuning and LoRA]]
