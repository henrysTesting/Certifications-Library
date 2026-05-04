---
tags: [concept, quantization, optimization, deployment]
exam: NCA-GENL
domain: Deployment and Optimization
---

# Quantization

Reducing the numerical precision of model weights to make models smaller, faster, and cheaper to run.

## Precision Formats

| Format | Bits | Notes |
|--------|------|-------|
| FP32 | 32 | Full precision; used in training |
| BF16 | 16 | Brain float; preferred for training/inference on modern GPUs |
| FP16 | 16 | Half precision; widely supported |
| INT8 | 8 | Common for inference; slight accuracy tradeoff |
| INT4 | 4 | Aggressive; used in QLoRA and edge deployment |

## Benefits

- **Smaller model size** — saves storage and GPU memory
- **Faster inference** — lower precision arithmetic is faster on CPUs, GPUs, and edge devices
- **Lower power consumption** — reduced heat production

## Types

| Type | Description |
|------|-------------|
| Post-Training Quantization (PTQ) | Quantize a trained model; fast but can lose accuracy |
| Quantization-Aware Training (QAT) | Train knowing the model will be quantized; better accuracy |

## Tradeoffs

- More aggressive quantization (INT4) = smaller/faster but more accuracy loss
- QAT recovers accuracy lost from PTQ
- For LLMs: FP16/BF16 is the sweet spot between performance and accuracy

## In NVIDIA's Stack

- TensorRT handles FP16/INT8 quantization for deployment
- QLoRA uses 4-bit base model weights for fine-tuning on consumer GPUs

## Related

- [[NVIDIA Ecosystem]]
- [[Fine-Tuning and LoRA]]
- [[Triton Inference Server]]
