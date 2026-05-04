---
tags: [concept, huggingface, tooling, python]
exam: NCA-GENL
domain: Software Development
---

# HuggingFace Transformers

Open-source Python library for working with LLMs and transformer-based models.

## Core Workflow

```
Pretrained Model → Tokenizer → Fine-tune or Infer → Deploy
```

## Key APIs

| API | Purpose |
|-----|---------|
| `pipeline()` | One-line API for common tasks: text-generation, classification, NER, summarization, translation |
| `AutoModel` | Auto-loads the correct model class for a given checkpoint |
| `AutoTokenizer` | Auto-loads the correct tokenizer for a given checkpoint |
| Model Hub | Repository of thousands of pretrained models |
| Datasets library | Access to public benchmark datasets |

## Supported Backends

PyTorch, TensorFlow, JAX

## Common `pipeline()` Tasks

```python
from transformers import pipeline

# Text generation
gen = pipeline("text-generation", model="gpt2")

# Classification
clf = pipeline("text-classification")

# NER
ner = pipeline("ner", aggregation_strategy="simple")

# Summarization
summ = pipeline("summarization")
```

## Exam Note

HuggingFace is the standard library for accessing pretrained models. Know that `pipeline()` provides one-line inference for common tasks, and that `AutoModel`/`AutoTokenizer` auto-select the right classes for any checkpoint.

## Related

- [[Transformer Architecture]]
- [[Fine-Tuning and LoRA]]
- [[Python Libraries]]
