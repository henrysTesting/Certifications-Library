---
tags: [concept, tokenization, nlp]
exam: NCA-GENL
domain: LLM Fundamentals
---

# Tokenization

The process of breaking raw text into units (tokens) the model can process numerically.

## Why Not Just Use Words?

- Rare words and proper nouns need coverage without an enormous vocabulary
- Subword tokenization handles morphology: `unbelievable → un-believ-able`
- Balances vocabulary size with representational power

## Common Tokenizers

| Tokenizer | Used By | Approach |
|-----------|---------|----------|
| Byte Pair Encoding (BPE) | GPT family | Merge frequent byte pairs iteratively |
| WordPiece | BERT | Similar to BPE; maximizes language model likelihood |
| SentencePiece | T5, LLaMA | Language-agnostic; treats text as raw bytes |

## Pipeline Position

Tokenization is step 1 of the transformer pipeline:
`Raw text → Tokens → Token IDs → Embeddings → Attention → Output`

## Key Facts for Exam

- A token ≠ a word; on average ~0.75 words per token in English
- Context window limits are measured in **tokens**, not words
- Same tokenizer must be used at training and inference time

## Related

- [[Transformer Architecture]]
- [[Embeddings]]
