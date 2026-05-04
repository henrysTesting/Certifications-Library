---
tags: [concept, ethics, trustworthy-ai, bias]
exam: NCA-GENL
domain: Trustworthy AI
---

# Trustworthy AI

## Core Ethical Principles

| Principle | Description |
|-----------|-------------|
| **Fairness** | Model should not discriminate based on protected attributes (race, gender, age) |
| **Transparency** | Users should understand how decisions are made (explainability) |
| **Accountability** | Humans remain responsible for AI outcomes |
| **Reliability / Safety** | System behaves correctly and predictably |
| **Privacy** | Personal data is protected and used appropriately |
| **Inclusivity** | AI benefits should be accessible broadly |

## Bias in AI

### Sources

| Source | Description |
|--------|-------------|
| Training data bias | Historical inequities in data replicate into model behavior |
| Label bias | Human annotators introduce their own biases |
| Sampling bias | Training data doesn't represent the full population |
| Algorithmic bias | Model architecture amplifies certain patterns |

### How to Minimize

- Diverse, representative training datasets
- Bias audits and fairness metrics (demographic parity, equalized odds)
- Human review for sensitive domains
- Data augmentation to balance underrepresented groups
- Regular re-evaluation as deployment context changes

## Data Privacy

- **Data minimization** — only collect data necessary for the task
- **Consent** — users must agree to how their data is used in training
- **Anonymization / differential privacy** — prevent re-identification of individuals
- **GDPR** — legal requirements around data storage, deletion, and usage

## Hallucinations and Trust

- Hallucinations undermine trustworthiness
- Mitigation: RAG + grounding + output validation + lower temperature
- Confidence scores and uncertainty estimation help users calibrate trust

## NVIDIA Technologies

| Tool | Purpose |
|------|---------|
| NeMo Guardrails | Safety rails for LLM apps; rules defined in Colang; prevents harmful/off-topic outputs |
| Triton + model versioning | Controlled rollouts and rollback if a model behaves unexpectedly |

## Related

- [[RLHF]]
- [[RAG]]
- [[NVIDIA Ecosystem]]
