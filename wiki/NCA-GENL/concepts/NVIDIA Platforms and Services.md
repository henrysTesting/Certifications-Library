---
tags: [concept, nvidia, cloud, platform, services]
exam: NCA-GENL
domain: NVIDIA AI Stack
---

# NVIDIA Platforms and Services

NVIDIA's platform and services layer sits above the hardware and software libraries, providing enterprise-ready deployment environments, pre-trained models, and specialized AI application SDKs.

---

## NVIDIA AI Enterprise

An **enterprise-certified AI software platform** — bundles NVIDIA's key software (NeMo, TensorRT, Triton, RAPIDS, etc.) with:
- Enterprise support, security patches, and stability guarantees.
- Certified to run on major cloud providers (AWS, Azure, GCP) and on-premises VMware environments.
- Simplifies deploying and scaling AI in **private / public / hybrid cloud** scenarios.

**Think of it as:** NVIDIA's "enterprise OS" for AI — the software layer that makes NVIDIA tools production-safe.

---

## NVIDIA NGC Catalog

An **official AI software hub** — the "app store" for NVIDIA-optimized AI resources.

| Resource Type | Examples |
|---|---|
| GPU-optimized containers | PyTorch, TensorFlow, NeMo, TensorRT-LLM containers |
| Pre-trained models | LLMs, vision models, speech models |
| Helm charts | Kubernetes deployment configurations |
| Industry SDKs | Clara (healthcare), Metropolis (vision AI), Riva |

- Accessed at `ngc.nvidia.com` or via `ngc` CLI.
- Containers include all optimized dependencies — pull and run immediately on NVIDIA hardware.
- Models are exported in formats compatible with TensorRT and Triton.

---

## NVIDIA DGX Cloud

A **managed AI supercomputing cloud service** — rent DGX-class compute without owning hardware.

- Launched in partnership with major CSPs: **Microsoft Azure, Google Cloud, Oracle Cloud**.
- Provides access to clusters of H100/H200 DGX systems on demand.
- Includes the full NVIDIA AI Enterprise software stack.
- Use case: Organizations needing occasional large-scale training runs without CapEx investment.

---

## NVIDIA AI Foundation Models

A **portfolio of pre-trained generative AI models** available through NGC and the NVIDIA API.

| Domain | Examples |
|---|---|
| Language (LLMs) | Nemotron, Llama variants with NVIDIA optimizations |
| Vision | Visual understanding, image generation |
| Biology | BioNeMo (protein structure, drug discovery) |
| Speech | Via Riva (ASR, TTS) |

- Available for **direct inference** (via NVIDIA API / cloud endpoints).
- Available for **fine-tuning** via NeMo — use as a starting checkpoint.
- Distributed through NGC; optimized for NVIDIA hardware.

---

## NVIDIA Riva

A **GPU-accelerated SDK for real-time conversational AI** applications.

| Capability | API |
|---|---|
| Automatic Speech Recognition (ASR) | Streaming transcription |
| Natural Language Processing (NLP) | Intent classification, entity extraction |
| Text-to-Speech (TTS) | Natural voice synthesis |

- Designed for **low-latency, real-time** voice applications.
- Runs on-premises (DGX), in the cloud, or at the edge (Jetson).
- Enterprise-grade: supports custom wake words, domain-specific vocabulary, multi-language.
- Part of the NVIDIA AI Enterprise suite.

---

## Ecosystem Map

```
Hardware (DGX / H100)
    ↓
Software (CUDA / NeMo / TensorRT-LLM / Triton)
    ↓
Platform (NVIDIA AI Enterprise)
    ↓
Distribution (NGC Catalog)
    ↓
Cloud (DGX Cloud)         Applications (Riva)
```

---

## Exam Notes

- **AI Enterprise** = certified enterprise bundle of NVIDIA software with support.
- **NGC** = model and container hub; first place to look for NVIDIA-optimized resources.
- **DGX Cloud** = rent DGX compute; partners with Azure, GCP, Oracle.
- **Riva** = speech + NLP SDK; ASR + TTS + NLP; GPU-accelerated real-time.
- Foundation Models can be used directly (inference) or fine-tuned (via NeMo).

---

## Related

- [[NeMo Framework]]
- [[Triton Inference Server]]
- [[NVIDIA Compute Systems]]
- [[NVIDIA Ecosystem]]
- [[Fine-Tuning and LoRA]]
