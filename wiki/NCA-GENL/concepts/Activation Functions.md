---
tags: [concept, neural-networks, activation]
exam: NCA-GENL
domain: LLM Fundamentals
---

# Activation Functions

Functions applied after a neuron's calculation step. Without them, the network behaves like a single linear calculator and cannot learn complex patterns.

## Common Functions

| Function | Range | Use Case | Key Property |
|----------|-------|----------|--------------|
| **ReLU** | [0, ∞) | Hidden layers | Outputs 0 for negatives; fast; avoids vanishing gradients |
| **Sigmoid** | (0, 1) | Binary output layer | Converts to probability; susceptible to vanishing gradients |
| **Softmax** | (0, 1) sum=1 | Multi-class output layer | Converts logits to probability distribution across classes |
| **Tanh** | (-1, 1) | Hidden layers (older) | Zero-centered version of sigmoid |

## Why ReLU Dominates Hidden Layers

- Simple and fast to compute
- Does not saturate for positive values → gradients flow freely
- Avoids the vanishing gradient problem that plagued sigmoid/tanh in deep networks

## Exam Quick Distinctions

- **ReLU** → hidden layers, deep networks
- **Sigmoid** → output layer, yes/no (binary classification)
- **Softmax** → output layer, pick one of many classes
- **Vanishing gradient** → sigmoid/tanh in deep nets; solved by ReLU + layer norm

## Related

- [[Backpropagation]]
- [[Transformer Architecture]]
