---
tags: [concept, neural-networks, training]
exam: NCA-GENL
domain: LLM Fundamentals
---

# Backpropagation & Neural Network Training

## Forward Propagation

Data flows through the network layer by layer to produce a prediction.

## Loss Function

Measures how far the prediction is from the ground truth.

- **Cross-entropy loss** — classification tasks
- **MSE (Mean Squared Error)** — regression tasks
- Lower loss = better model fit

## Gradient

Tells us how much and in which direction to change a model's parameters to reduce error.

- **Large gradient** → make a big change to weights
- **Small gradient** → make a small change
- **Zero gradient** → no learning happens

## Backpropagation

Propagates the loss gradient backward through the network layer by layer, computing each weight's contribution to the error. Weights are then updated via gradient descent.

```
Forward pass → compute loss → backward pass (gradients) → update weights
```

## Key Problems

| Problem | Description | Solution |
|---------|-------------|----------|
| Vanishing gradients | Gradient becomes tiny in deep networks; early layers stop learning | ReLU, layer normalization, residual connections |
| Exploding gradients | Gradient grows uncontrollably; training diverges | Gradient clipping, layer normalization |

## Layer Normalization

Standardizes outputs from each layer to a consistent range (~[-3, +3]).
- Prevents exploding gradients in deep networks
- Keeps training stable as depth increases
- Used in every transformer block

## Hyperparameters

Configured before training begins:

| Hyperparameter | Effect |
|---------------|--------|
| Learning rate | How big each weight update step is; too high = diverge, too low = slow |
| Batch size | Samples processed per update; affects stability and speed |
| Number of epochs | Full passes through training data |

## Related

- [[Activation Functions]]
- [[Transformer Architecture]]
