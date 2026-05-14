---
tags: [concept, privacy, trustworthy-ai, compliance]
exam: NCA-GENL
domain: Trustworthy AI
---

# Data Privacy and Consent

The legal, ethical, and technical requirements for handling personal data in AI systems, including regulatory compliance and the principles governing when data may be collected and used.

---

## Core Frameworks

### GDPR (General Data Protection Regulation)

- **Jurisdiction:** European Union
- **Scope:** Any organization processing EU residents' personal data, regardless of where the org is located
- **Key rights:** Right to access, right to rectification, right to erasure ("right to be forgotten"), right to portability, right to object

**Key GDPR principles for AI:**
- Data minimization — collect only what is necessary
- Purpose limitation — use data only for the stated purpose
- Storage limitation — retain data no longer than needed
- Accuracy — keep data up to date

### CCPA (California Consumer Privacy Act)

- **Jurisdiction:** California, USA
- **Scope:** Businesses collecting California residents' personal information above certain thresholds
- **Key rights:** Right to know, right to delete, right to opt-out of data sale, non-discrimination

| Framework | Region | Key Mechanism |
|-----------|--------|--------------|
| GDPR | EU/EEA | Consent + legitimate interest; DPA oversight |
| CCPA | California | Opt-out model; right to know and delete |

---

## CIA Triad (Information Security)

Foundational security model applicable to AI data pipelines:

| Property | Definition | Example Threat |
|----------|-----------|---------------|
| **Confidentiality** | Data accessible only to authorized parties | Data breach, unauthorized model access |
| **Integrity** | Data is accurate and unaltered | Training data poisoning, adversarial inputs |
| **Availability** | Data/system accessible when needed | DDoS attacks, infrastructure failures |

AI systems must address all three — a model trained on poisoned (integrity-violated) data produces unreliable outputs even if confidentiality is intact.

---

## Consent Principles

For data collection to be lawful under GDPR, consent must be:

| Principle | Requirement |
|-----------|------------|
| **Freely given** | No coercion or significant imbalance of power |
| **Specific** | Purpose must be clearly stated; blanket consent is insufficient |
| **Informed** | Data subject must understand what they're consenting to |
| **Unambiguous** | Opt-in only; pre-ticked boxes are not valid consent |

**Withdrawable:** Consent can be withdrawn at any time as easily as it was given.

---

## Privacy-Preserving Techniques in AI

| Technique | How It Works | Use Case |
|-----------|-------------|----------|
| **Federated learning** | Train on local data; share only gradients, not raw data | Healthcare, mobile devices |
| **Differential privacy** | Add calibrated noise to training data/gradients | Prevent membership inference attacks |
| **Data anonymization** | Remove or generalize PII before use | Dataset release, research |
| **Synthetic data** | Generate artificial data with same statistical properties | Training data augmentation without privacy risk |

**NVIDIA tools:**
- NVIDIA AI Enterprise — supports privacy-compliant deployment workflows
- NVIDIA Omniverse — synthetic data generation for training without real-world PII

---

## Privacy Risks in LLMs

- **Memorization** — LLMs can memorize and regurgitate training data verbatim, including PII
- **Model inversion** — adversary reconstructs training data from model outputs
- **Membership inference** — attacker determines whether a specific record was in training data

**Mitigation:** Differential privacy during training, careful data curation, output filtering

---

## Exam Notes

- **GDPR consent must be:** Freely given, specific, informed, and unambiguous
- **What is the CIA triad?** → Confidentiality, Integrity, Availability
- **CCPA vs. GDPR:** CCPA uses opt-out; GDPR requires opt-in consent
- **Federated learning preserves privacy by:** Keeping raw data local; only sharing model updates (gradients)
- **Differential privacy:** Adds noise to prevent individual data points from being reconstructable
- **"Right to be forgotten"** → GDPR; requires ability to delete individual's data and retrain or adjust model

---

## Related

- [[Trustworthy AI]] — broader ethical principles; fairness; human oversight
- [[AI Bias Minimization]] — data quality and bias in collected datasets
- [[NeMo Framework]] — NeMo Guardrails for output safety
