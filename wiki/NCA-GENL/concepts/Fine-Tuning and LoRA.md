---
tags: [concept, fine-tuning, lora, peft]
exam: NCA-GENL
domain: Generative AI Concepts
---

# Fine-Tuning and LoRA

## Fine-Tuning

Retraining a pre-trained model on a new, task-specific dataset to improve performance on that task.

### Types

| Type | Description |
|------|-------------|
| Full fine-tuning | Update all model weights; most powerful, most expensive |
| Parameter-efficient (PEFT) | Update only a small subset of weights; cheaper |
| LoRA | Inject small adapter matrices; freeze original weights |
| QLoRA | LoRA + quantization; enables fine-tuning on consumer hardware |
| Prompt learning | Learn soft prompt embeddings; no weight changes |

### When to Fine-Tune (vs. RAG vs. Prompt Engineering)

- Use fine-tuning when you need specialized behavior, style, or domain knowledge baked into the model
- Use RAG when you need access to dynamic or private data without retraining
- Use prompt engineering first — cheapest and fastest to iterate

## LoRA (Low-Rank Adaptation)

Parameter-efficient fine-tuning that injects small trainable rank-decomposition matrices into attention layers.

### How It Works

1. Original model weights are **frozen**
2. Two small matrices `A` and `B` are injected alongside each weight matrix: `ΔW = A × B`
3. Only `A` and `B` are trained — drastically fewer parameters
4. At inference: `W_effective = W_original + ΔW`

### Benefits

- Drastically reduces memory and compute needed for fine-tuning
- Multiple LoRA adapters can be swapped on a single base model
- QLoRA extends this to 4-bit quantized base models — enables fine-tuning on a single GPU

## Knowledge Distillation

A large **teacher** model transfers its knowledge to a smaller **student** model.
- Student learns to mimic teacher's output distribution, not just labels
- Result: compact model that approximates the capability of the large one

## Related

- [[RLHF]]
- [[RAG]]
- [[Prompt Engineering]]
- [[Quantization]]
