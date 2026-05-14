---
tags: [concept, training, regularization]
exam: NCA-GENL
domain: LLM Fundamentals
sources: 0
---

# Regularization Techniques for LLMs

## Overview

Regularization techniques prevent a model from overfitting by constraining what it learns during training. They force the model to generalize rather than memorize the training data.

## Primary Techniques

### Dropout

Randomly deactivates a fraction of neurons during training to prevent co-adaptation.

- **How it works:** During each forward pass, drop a percentage (typically 10–50%) of activations to zero
- **Effect:** Forces network to learn redundant representations; no single neuron becomes responsible for capturing a pattern
- **At inference:** Use all neurons (optionally scaled by dropout rate)
- **When to use:** Most effective in dense layers; less critical in attention layers due to their inherent diversity
- **Exam relevance:** Dropout is the most commonly tested regularization technique for LLM overfitting

### Weight Decay (L1/L2 Regularization)

Adds a penalty term to the loss function proportional to the magnitude of weights.

| Type | Formula | Effect |
|------|---------|--------|
| L2 (Ridge) | Loss + λ × (sum of squared weights) | Shrinks all weights slightly; preferred for neural networks |
| L1 (Lasso) | Loss + λ × (sum of absolute weights) | Drives some weights to exactly zero; sparsity |

- **λ (lambda):** Regularization strength; tuned as a hyperparameter
- **Effect:** Prevents weights from growing too large; encourages simpler solutions

### Early Stopping

Monitor validation loss and halt training when it stops improving.

- **How it works:** Track validation perplexity/loss during training; stop if it doesn't improve for N epochs
- **Effect:** Prevents overfitting by avoiding unnecessary training epochs
- **Trade-off:** May underfit if stopped too early; requires a held-out validation set

### Data Augmentation

Artificially expand the training set or add noise to prevent the model from memorizing exact inputs.

- **Token-level:** Mask or shuffle tokens; substitute synonyms
- **Sentence-level:** Paraphrase, back-translation, or mixup
- **Effect:** Increases effective training data diversity without retraining from scratch

## Common Exam Misconceptions

| Statement | Verdict | Explanation |
|-----------|---------|-------------|
| "Increasing model size reduces overfitting" | **False** | Larger models have more capacity to memorize; they overfit *more* easily |
| "Dropout prevents underfitting" | **False** | Dropout is purely an anti-overfitting tool; it can't help a model that's too simple |
| "Smaller batch size helps generalization" | **False** | Smaller batches introduce noise and *increase* overfitting risk |
| "Lower learning rate prevents overfitting" | **Misleading** | A lower learning rate slows training but doesn't inherently prevent overfitting; given enough epochs, the model will still overfit |
| "Dropout is the only regularization technique needed" | **False** | Best results come from combining multiple techniques (dropout + weight decay + early stopping) |

## Diagnosing Overfitting

Use [[Perplexity and Model Fitting]] to identify overfitting:

- **Training perplexity:** Very low (model fits training data well)
- **Validation/test perplexity:** High (model fails to generalize)
- **Gap between train and test:** Large → overfitting present

## Choosing Regularization Strategies

| Scenario | Best Approach |
|----------|---------------|
| Training loss decreases, validation loss increases | Early stopping + dropout |
| All weights grow very large | Weight decay (L2) |
| Need interpretability / sparse solutions | L1 regularization |
| Small training dataset | Early stopping + aggressive dropout + data augmentation |
| Large, diverse dataset | Lighter regularization (smaller dropout rate, lower λ) |

## Related

- [[Perplexity and Model Fitting]]
- [[Backpropagation]]
- [[Fine-Tuning and LoRA]]
- [[Model Evaluation Metrics]]
