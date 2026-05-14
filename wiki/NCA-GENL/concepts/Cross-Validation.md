---
tags: [concept, cross-validation, experimentation, model-evaluation]
exam: NCA-GENL
domain: Experimentation
---

# Cross-Validation

A model evaluation technique that tests generalization by training and evaluating on multiple held-out subsets of the data, rather than a single train/test split.

---

## Why Cross-Validation?

A single train/test split can give misleading results depending on how data was partitioned. Cross-validation averages performance across multiple splits to produce a more robust estimate of generalization error.

**Primary purpose:** Detect and prevent overfitting without sacrificing training data.

---

## Techniques

### K-Fold Cross-Validation

1. Split data into **k** equal-sized folds
2. Train on k−1 folds, evaluate on the held-out fold
3. Repeat k times, rotating the held-out fold
4. Final score = average across all k evaluations

**Typical k values:** 5 or 10
**Tradeoff:** Higher k → lower bias, higher variance, more compute

```
Data: [Fold1 | Fold2 | Fold3 | Fold4 | Fold5]

Run 1: Train=[2,3,4,5]  Test=[1]
Run 2: Train=[1,3,4,5]  Test=[2]
Run 3: Train=[1,2,4,5]  Test=[3]
...
```

### Stratified K-Fold

Same as k-fold but each fold preserves the **class distribution** of the original dataset.

**Use when:** Classification tasks with imbalanced classes
**Why:** Prevents folds from having no minority-class examples

### Leave-One-Out Cross-Validation (LOOCV)

Special case where k = n (one sample held out per iteration).

| Property | Value |
|----------|-------|
| Bias | Very low |
| Variance | High |
| Compute | Very expensive (n training runs) |
| Best for | Very small datasets |

### Hold-Out Validation

Simple train/validation/test split (e.g., 70/15/15).
- Fastest; used when data is abundant
- Not technically cross-validation — just a baseline approach

---

## Cross-Validation vs. Single Split

| Aspect | Single Split | K-Fold CV |
|--------|-------------|-----------|
| Variance of estimate | High | Low |
| Bias of estimate | Depends on split | Lower |
| Data efficiency | Wastes validation data | Uses all data |
| Compute cost | Low | k× higher |

---

## Nested Cross-Validation

Used for **simultaneous hyperparameter tuning and model evaluation**:
- Outer loop: estimate generalization error
- Inner loop: tune hyperparameters

Prevents optimistic bias from tuning on the same data used for evaluation.

---

## Exam Notes

- **K-fold is the default recommendation** for general model evaluation
- **Stratified k-fold** is correct when classes are imbalanced
- **LOOCV** is correct for very small datasets
- Cross-validation is a technique to **prevent overfitting**, not cure it — still need regularization
- Cross-validation estimates the **expected generalization performance**, not a guarantee
- Watch for: "Which cross-validation method preserves class balance?" → Stratified k-fold

---

## Related

- [[Regularization Techniques for LLMs]] — complementary overfitting prevention
- [[Perplexity and Model Fitting]] — diagnosing over/underfitting after training
- [[Model Evaluation Metrics]] — the metrics computed within each fold
- [[Feature Engineering]] — cross-validate after feature engineering to avoid leakage
