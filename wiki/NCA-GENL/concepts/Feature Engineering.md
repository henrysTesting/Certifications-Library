---
tags: [concept, feature-engineering, data-analysis, ml]
exam: NCA-GENL
domain: Data Analysis
---

# Feature Engineering

The process of transforming raw data into features that better represent the underlying problem, improving model performance.

---

## Why It Matters

Raw data is rarely ready for modeling. Feature engineering bridges the gap between raw inputs and the model's ability to learn patterns.

---

## Core Techniques

### Handling Missing Values

| Strategy | When to Use |
|----------|-------------|
| Mean/median imputation | Numerical; low missing rate; approximately symmetric |
| Mode imputation | Categorical features |
| Forward/backward fill | Time series data |
| Drop rows/columns | Very high missing rate (>40-50%) |
| Model-based imputation | Complex relationships between features |

### Encoding Categorical Variables

| Method | Description | Best For |
|--------|-------------|----------|
| One-hot encoding | Binary column per category | Low-cardinality, no ordinal relationship |
| Label encoding | Integer per category | Ordinal categories; tree-based models |
| Target encoding | Replace category with target mean | High-cardinality; risk of leakage |
| Embedding | Learned dense vector | Neural nets; high-cardinality |

### Feature Scaling

| Method | Formula | Best For |
|--------|---------|----------|
| StandardScaler (Z-score) | (x − μ) / σ | Normally distributed; SVM, linear models, PCA |
| MinMaxScaler | (x − min) / (max − min) | Bounded range [0,1]; neural nets; KNN |
| RobustScaler | (x − median) / IQR | Data with significant outliers |
| Log transform | log(x + 1) | Skewed distributions |

**Rule of thumb:** Tree-based models (decision trees, random forests) are scale-invariant — scaling doesn't help them. Distance-based and gradient-based models require scaling.

### Feature Selection

| Technique | Type | Notes |
|-----------|------|-------|
| Correlation matrix | Filter | Remove highly correlated features (multicollinearity) |
| Variance threshold | Filter | Remove near-zero variance features |
| Mutual information | Filter | Non-linear dependency measure |
| L1 regularization (Lasso) | Embedded | Shrinks weak feature weights to 0 |
| Recursive Feature Elimination (RFE) | Wrapper | Iteratively removes least important features |
| PCA | Dimensionality reduction | Unsupervised; creates new orthogonal features |

### Binning / Discretization

Convert continuous variables into discrete buckets:
- **Equal-width binning** — fixed interval size; sensitive to outliers
- **Equal-frequency binning** — same number of samples per bin; handles skew
- **Domain-based binning** — bins defined by domain knowledge (e.g., age groups)

Use when: linear models struggle with non-linear continuous relationships; decision trees benefit from natural cutpoints.

---

## Feature Engineering for NLP

- **Bag of Words (BoW)** — count or binary presence of words; loses order
- **TF-IDF** — term frequency × inverse document frequency; down-weights common words
- **N-grams** — capture adjacent word sequences (bigram, trigram)
- **Word embeddings** — dense vectors encoding semantic meaning (see [[Text Embedding Models]])

---

## Common Exam Patterns

- **What technique prevents dominance of high-magnitude features?** → Feature scaling (StandardScaler or MinMaxScaler)
- **What handles high-cardinality categorical features in neural nets?** → Embeddings
- **What removes irrelevant or redundant features automatically during training?** → L1 regularization (Lasso)
- **PCA use case** → Reduce dimensionality, remove correlated features, speed up training

---

## Related

- [[Python Libraries]] — scikit-learn's `StandardScaler`, `MinMaxScaler`, `OneHotEncoder`, `RFE`
- [[Regularization Techniques for LLMs]] — L1/L2 regularization applied to features
- [[Text Embedding Models]] — feature engineering for NLP
- [[Cross-Validation]] — evaluating model performance after feature engineering
