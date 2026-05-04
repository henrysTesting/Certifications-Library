---
tags: [concept, attention, transformer]
exam: NCA-GENL
domain: LLM Fundamentals
---

# Attention Mechanism

Highlights the most relevant parts of the input for generating each output token. The core innovation that made transformers scale.

## How It Works

- Each token produces a **query**, **key**, and **value** vector
- Attention score = similarity between a token's query and all other tokens' keys
- Scores are softmaxed into weights; output = weighted sum of value vectors
- Result: each token's representation is influenced by all tokens it is relevant to

## Multi-Head Attention

- Runs multiple attention operations in parallel ("heads")
- Each head learns to track a different type of relationship (syntactic, semantic, coreference, etc.)
- More heads → richer relational modeling
- Outputs from all heads are concatenated and projected

## Why It Matters

- Replaces recurrence (RNNs/LSTMs) with direct token-to-token connections
- No sequential bottleneck → enables parallel training
- Captures long-range dependencies that RNNs struggled with

## KV Cache (Inference)

- At inference time, key and value vectors are cached for previously seen tokens
- Avoids recomputing attention over the full context on every new token
- Critical for latency and throughput in deployed LLMs
- See [[Quantization]] for memory tradeoffs

## Related

- [[Transformer Architecture]]
- [[KV Cache]]
