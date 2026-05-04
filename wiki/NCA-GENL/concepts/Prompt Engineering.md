---
tags: [concept, prompting, genai]
exam: NCA-GENL
domain: Generative AI Concepts
---

# Prompt Engineering

Designing inputs to LLMs to steer output toward a desired format, tone, or answer — without changing model weights.

## Techniques

| Technique | Description |
|-----------|-------------|
| Zero-shot | No examples; model uses only pre-trained knowledge |
| One-shot | One example in the prompt |
| Few-shot | 2–10 examples; most reliable for complex tasks |
| Chain-of-thought (CoT) | Include step-by-step reasoning examples to elicit reasoning |
| System prompt | Sets the persona/role/constraints of the model |

## Key Parameters

| Parameter | Effect |
|-----------|--------|
| **Temperature** | Controls randomness: 0 = deterministic, 1+ = creative |
| **Top-p (nucleus sampling)** | Limits token selection to top cumulative probability mass |
| **Top-k** | Limits token selection to top-k most probable tokens |

## Best Practices

- Be specific and clear about the task
- Provide context and constraints
- Use examples (few-shot) to steer format and tone
- Iterate: test → observe output → adjust prompt
- For complex tasks, chain-of-thought prompting improves reasoning quality

## When to Use vs. Alternatives

| Approach | When to Use |
|----------|-------------|
| Prompt engineering | Simple tasks, generic use cases, no retraining budget |
| RAG | Need access to private/current data |
| Fine-tuning | Need specialized behavior baked into the model |

## Related

- [[RAG]]
- [[Fine-Tuning and LoRA]]
- [[Inference Parameters]]
