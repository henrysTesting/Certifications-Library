---
tags: [concept, diffusion, generative-ai]
exam: NCA-GENL
domain: Generative AI Concepts
---

# Diffusion Models

Generative models that learn to reverse a noise-adding process to produce realistic data.

## Core Idea

Instead of memorizing data, the model learns how real data differs from random noise.

## Two Phases

| Phase | Description |
|-------|-------------|
| **Forward diffusion (training)** | Progressively add noise to clean data; model sees all stages of corruption and learns the data structure |
| **Reverse diffusion (inference)** | Model learns to undo the noise; removes noise step by step to reconstruct realistic output |

## Contrast with Autoregressive Models

| | Diffusion | Autoregressive (GPT) |
|--|-----------|---------------------|
| Output | Images, audio | Text |
| Generation | Iterative denoising | Token by token |
| Training signal | Predict noise | Predict next token |

## Use Cases

- Image generation: Stable Diffusion, DALL-E
- Audio synthesis
- Video generation

## Exam Note

Diffusion models are mentioned in the notes primarily as a contrast to transformer-based LLMs. For the NCA-GENL exam, know the basic mechanism (forward noise → reverse denoise) and that they are used for non-text modalities.

## Related

- [[Transformer Architecture]]
- [[Generative AI Concepts]]
