---
tags: [concept, bias, trustworthy-ai, fairness]
exam: NCA-GENL
domain: Trustworthy AI
---

# AI Bias Minimization

The systematic identification, measurement, and reduction of bias in AI systems to ensure fair, equitable, and accurate outputs across diverse populations.

---

## Types of Bias

### Data Bias

Bias originating from the training data itself:

| Subtype | Description | Example |
|---------|-------------|---------|
| **Sampling bias** | Training data does not represent the target population | Facial recognition trained mostly on lighter-skinned faces |
| **Historical bias** | Reflects and encodes past societal inequities | Resume screening trained on historical hires (mostly male in tech) |
| **Measurement bias** | Systematic error in how features or labels were recorded | Labels assigned differently across demographic groups |
| **Aggregation bias** | One model applied to groups with different underlying patterns | Single medical diagnostic model for all ethnic groups |

### Algorithm Bias

Bias introduced or amplified by the model architecture, objective function, or training process:
- Objective functions that optimize for overall accuracy may sacrifice minority-group performance
- Embedding spaces encode societal biases present in training corpora
- Feedback loops: biased predictions → biased data collection → reinforced bias

### Interaction Bias

Bias arising from user interaction with deployed systems:
- Users may interact differently with AI depending on perceived identity of the AI
- Chatbots trained on interaction logs inherit the biases of users who provided the training signal
- RLHF annotator bias: human preference labels reflect annotator demographics and values

---

## Bias Detection

| Method | Description |
|--------|-------------|
| **Disaggregated evaluation** | Measure performance metrics separately per demographic group |
| **Fairness metrics** | Demographic parity, equalized odds, individual fairness |
| **Counterfactual testing** | Change only a protected attribute and compare outputs |
| **Embedding bias probes** | Test word association biases in embedding space (WEAT test) |

---

## Mitigation Strategies

### Pre-processing (Data Level)

- Collect **diverse, representative datasets**
- Rebalance underrepresented groups (oversampling, SMOTE)
- Remove or anonymize protected attributes
- Use **NVIDIA Omniverse Replicator** for synthetic diverse data generation

### In-processing (Model Level)

- **Fairness-aware algorithms** — incorporate fairness constraints into the training objective
- **Adversarial debiasing** — add an adversary that predicts protected attributes; penalize if it succeeds
- Regularization terms that penalize disparate impact

### Post-processing (Output Level)

- Threshold adjustment per group to equalize error rates
- Output filtering and guardrails (see [[NeMo Framework]])

---

## Explainability Tools (XAI)

Explainability helps detect and diagnose bias by revealing which features drove a prediction:

| Tool | Method | Output |
|------|--------|--------|
| **SHAP** (SHapley Additive exPlanations) | Game-theoretic feature attribution | Per-feature contribution to each prediction |
| **LIME** (Local Interpretable Model-Agnostic Explanations) | Local surrogate model | Approximate local decision boundary |
| **Model Cards** | Structured documentation | Bias evaluation results, intended use, limitations |

**SHAP vs. LIME:**
- SHAP is globally consistent and theoretically grounded; slower
- LIME is faster and more flexible; less consistent across runs

---

## NVIDIA Tools for Bias Mitigation

| Tool | Role |
|------|------|
| **NVIDIA Omniverse Replicator** | Generate synthetic training data with controlled demographic diversity |
| **NeMo Guardrails** | Runtime output filtering to prevent biased or harmful responses |
| **NVIDIA AI Enterprise** | Governance workflows for bias auditing and model provenance |
| **Federated learning** | Train across diverse data silos without centralizing potentially biased data |

---

## The Trustworthy AI Principles Connection

Bias minimization operationalizes the EU AI ethics principles:
- **Fairness & non-discrimination** — bias minimization directly addresses this
- **Explicability** — XAI tools enable auditing for bias
- **Human oversight** — human-in-the-loop review of high-stakes biased decisions
- **Diversity, non-discrimination & fairness** — one of the 7 EU HLEG key requirements

See [[Trustworthy AI]] for the full framework.

---

## Exam Notes

- **Three bias types:** Data bias, algorithm bias, interaction bias
- **Data bias subtypes to know:** Sampling, historical, measurement
- **Which tool provides per-feature contribution scores?** → SHAP
- **Synthetic data generation for diverse training sets:** NVIDIA Omniverse Replicator
- **Fairness-aware algorithms address:** Algorithm bias during training
- **Model Cards serve what purpose?** → Document a model's intended use, performance across groups, and known limitations — transparency artifact
- **RLHF bias source:** Annotator demographics and values embedded in preference labels

---

## Related

- [[Trustworthy AI]] — ethical principles, human oversight, lawful/ethical/robust framework
- [[Data Privacy and Consent]] — data governance; diverse data collection must respect privacy
- [[RLHF]] — human feedback introduces interaction/annotator bias
- [[NeMo Framework]] — NeMo Guardrails for output filtering
- [[Model Evaluation Metrics]] — disaggregated evaluation to detect bias
