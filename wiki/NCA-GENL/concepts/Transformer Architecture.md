---
tags: [concept, transformer, architecture]
exam: NCA-GENL
domain: LLM Fundamentals
---

# Transformer Architecture

Deep learning models that understand relationships within sequences. The foundation of modern LLMs.

## Why Powerful

- **Parallel processing** — processes all tokens simultaneously (unlike RNNs)
- **Flexible attention** — any token can attend to any other token
- **Scalable architecture** — more parameters = more capability

## Building Blocks

| Block | Role |
|-------|------|
| Embeddings | Convert tokens into numeric vectors |
| Self-attention | Lets tokens influence each other |
| Feed-forward layers | Refine and transform token representations |
| Layer normalization | Stabilizes training; keeps values in ~[-3, +3] range |

## Token Processing Pipeline

1. **Tokenization** — break phrase into subword tokens (BPE / SentencePiece / WordPiece)
2. **Encoding** — tokens mapped to numerical IDs
3. **Word embedding** — token IDs → dense vectors; positional encoding adds word order
4. **Attention / Decoding** — self-attention + learned patterns predict next token
5. **Output** — predicted tokens converted back to text

## Encoder vs. Decoder vs. Encoder-Decoder

| Type | Use Case | Example |
|------|----------|---------|
| Encoder only | Classification, NER, QA, understanding | BERT |
| Decoder only | Generation: chat, code, story writing | GPT, LLaMA |
| Encoder-Decoder | Translation, summarization, paraphrase | T5, BART |

## Prediction Strategies

- **Autoregressive** — generates one token at a time conditioned on prior tokens (GPT)
- **Masked (bidirectional)** — fills blanks using both left and right context (BERT MLM)
- **Denoising / text-to-text** — reconstruct text into a different form (T5)
- **Sequence-to-sequence** — generate new sequence one token at a time

## Related

- [[Attention Mechanism]]
- [[Tokenization]]
- [[Embeddings]]
- [[BERT]]
