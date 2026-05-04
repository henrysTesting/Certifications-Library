---
tags: [concept, rlhf, alignment]
exam: NCA-GENL
domain: Generative AI Concepts
---

# RLHF (Reinforcement Learning from Human Feedback)

Training process that aligns LLM output with human preferences. Used in ChatGPT, Claude, and Gemini.

## Steps

1. **Supervised Fine-Tuning (SFT)** — fine-tune base model on high-quality human-written demonstrations
2. **Reward Model Training** — collect human preference comparisons (response A vs. B); train a reward model to predict which response humans prefer
3. **RL Optimization (PPO)** — use the reward model as a signal; optimize the LLM policy using Proximal Policy Optimization (PPO) to generate outputs that score higher

## Why It Matters

- Raw pre-trained models optimize for next-token prediction, not helpfulness or safety
- RLHF bridges the gap between "predicts likely text" and "gives useful, safe answers"
- Enables instruction following, refusal of harmful requests, and tonally appropriate responses

## Limitations

- Expensive: requires large amounts of human preference data
- Reward hacking: model learns to game the reward model without genuinely improving
- Reward model can encode annotator biases

## Alternative: Constitutional AI (CAI)

- Anthropic's approach: instead of human comparisons, use a set of principles (a "constitution")
- Model critiques and revises its own outputs against the principles
- Reduces reliance on human labelers

## Related

- [[Fine-Tuning and LoRA]]
- [[Trustworthy AI]]
