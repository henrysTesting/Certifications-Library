---
tags: [domain, llm, fundamentals]
exam: NCA-GENL
sources: 2
---

# LLM Fundamentals

## Core Topics

- **Transformer architecture** — attention mechanism, encoder/decoder, self-attention
- **Tokenization** — BPE, WordPiece, SentencePiece; tokens vs words
- **Embeddings** — vector representations, semantic similarity, embedding space
- **Pretraining** — next-token prediction, masked language modeling, data scale
- **Context window** — max token length, positional encoding
- **Parameters** — model size, weight matrices, what "7B" means
- **Activation functions** — ReLU (hidden layers), Sigmoid (binary output), Softmax (multi-class)
- **Backpropagation** — gradients, loss functions, vanishing/exploding gradients, layer normalization
- **Feature engineering** — missing value handling, encoding (one-hot, label, target), scaling (StandardScaler, MinMaxScaler), feature selection, binning
- **Cross-validation** — k-fold, stratified k-fold, LOOCV; prevents overfitting; generalization estimation
- **Text embedding models** — Word2Vec (CBOW/Skip-gram), GloVe, FastText (n-gram subwords), BERT, SBERT, USE; static vs. contextual
- **Loss functions** — MSE (sensitive to outliers), MAE (robust), binary cross-entropy, categorical cross-entropy
- **Traditional ML** — logistic regression, SVM, decision trees, random forests, k-means, PCA; scikit-learn ecosystem

## Concept Pages

- [[Transformer Architecture]]
- [[Tokenization]]
- [[Embeddings]]
- [[Attention Mechanism]]
- [[Activation Functions]]
- [[Backpropagation]]
- [[BERT]]
- [[Feature Engineering]]
- [[Cross-Validation]]
- [[Text Embedding Models]]

## Sources

- [[GenAINotes]] — Modules 2, 3, 4, 10 + Domain 1 supplement
- [[NVIDIA-NCA-GENL-Master-Cheat-Sheet]] — Domain 1 (Core ML & AI Knowledge, 30%); feature engineering, cross-validation, text embeddings, traditional ML, loss functions
