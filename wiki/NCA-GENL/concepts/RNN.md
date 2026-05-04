---
tags: [concept, neural-networks, architecture]
exam: NCA-GENL
domain: LLM Fundamentals
---

# Recurrent Neural Networks (RNN)

## Definition

A **Recurrent Neural Network (RNN)** is a class of neural networks designed to process **sequential data** by maintaining an internal state (hidden state) that updates as it processes each element in a sequence. Unlike feedforward networks that process all input independently, RNNs have **connections that loop back**, allowing information to persist across time steps.

## How RNNs Work

### Core Mechanism

At each time step `t`, an RNN computes:
- **Hidden state**: `h_t = activation(W_h * h_{t-1} + W_x * x_t + b)`
- **Output**: `y_t = W_y * h_t + b_y`

Where:
- `h_{t-1}` = hidden state from previous step (the "memory")
- `x_t` = input at current step
- `W_h`, `W_x`, `W_y` = weight matrices (shared across all time steps)
- `activation` = typically tanh or ReLU

The **recurrent connection** `h_{t-1} → h_t` is what enables RNNs to "remember" information from previous steps.

### Training: Backpropagation Through Time (BPTT)

RNNs are trained using **Backpropagation Through Time (BPTT)**, which unrolls the network across time steps and applies [[Backpropagation]] to the unrolled graph.

**Challenge**: **Vanishing/Exploding Gradients**
- Gradients shrink exponentially as they flow backward through many time steps (vanishing gradient)
- Or explode if weights are large enough
- Limits RNN's ability to capture long-range dependencies (typically 10–20 steps)

## RNN Variants

### LSTM (Long Short-Term Memory)
- Uses **gates** (forget, input, output) to control information flow
- Solves vanishing gradient problem via cell state (long-term memory)
- Can capture dependencies 100+ steps away
- Industry standard before transformers

### GRU (Gated Recurrent Unit)
- Simplified LSTM with fewer gates (reset and update)
- Fewer parameters, faster to train
- Similar performance to LSTM

### Bidirectional RNN (BiRNN)
- Processes sequence forward AND backward
- Captures context from both directions
- Used in [[BERT]] (encoder-only model)

## Best Use Cases

| Use Case | Why RNNs Excel | Example |
|----------|----------------|---------|
| **Time series forecasting** | Captures temporal patterns and dependencies | Stock prices, weather, sensor readings |
| **Machine translation** | Encoder-decoder architecture processes sequential tokens | Sequence-to-sequence models (pre-transformer era) |
| **Speech recognition** | Processes audio frames in sequence | Converting waveforms to text |
| **Text generation & language modeling** | Next-token prediction with sequential context | Character/word-level generation |
| **Named entity recognition (NER)** | BiRNN tags words with context from both directions | Identifying people, places, organizations |
| **Sentiment analysis** | Preserves word order and context | Classifying review polarity |
| **Handwriting recognition** | Temporal structure of pen strokes | Online handwriting input |

## Advantages

✓ **Handles variable-length sequences** — no fixed input size  
✓ **Parameter efficiency** — weights shared across time steps  
✓ **Captures sequential patterns** — naturally models temporal relationships  
✓ **Bidirectional variants** — can use full context  

## Limitations

✗ **Vanishing/exploding gradients** — limits long-range dependencies (LSTM/GRU mitigate this)  
✗ **Slow training** — BPTT is computationally expensive; sequential processing hard to parallelize  
✗ **Long-range dependencies** — still struggle compared to transformers with [[Attention Mechanism]]  
✗ **Scalability** — difficult to parallelize across time steps  

## RNN vs. Transformers

| Aspect | RNN | [[Transformer Architecture]] |
|--------|-----|-------------------------|
| **Parallelization** | Sequential (slow) | Parallel (fast) |
| **Long-range dependencies** | Limited (~100s tokens with LSTM) | Unlimited (all tokens attend to all) |
| **Training speed** | Slow | Fast |
| **Inference latency** | Low | Higher (full sequence attention) |
| **Memory** | O(hidden_size) | O(n²) where n=sequence length |
| **Context window** | Naturally unbounded but practically limited | Fixed but can be very large |

**Modern LLMs use [[Transformer Architecture]]** because of superior parallelization, speed, and ability to capture long-range dependencies. [[Attention Mechanism|Transformers' self-attention]] has largely superseded RNNs for NLP tasks.

## Legacy & Current Relevance

- **Historical importance**: Dominated NLP/speech before 2017–2018
- **Still used for**: Real-time, low-latency applications; streaming data; embedded systems
- **Exam context**: Understanding RNNs is foundational to understanding why transformers were a breakthrough
- **Modern applications**: RNNs appear in specialized architectures (e.g., temporal models, anomaly detection)

## Key Takeaway

RNNs are the **classic sequential model** — simple, parameter-efficient, but limited by gradient flow and slow parallelization. LSTMs/GRUs fixed gradient issues, but transformers with [[Attention Mechanism|attention]] are now preferred for most NLP tasks due to speed and long-range dependency modeling.
