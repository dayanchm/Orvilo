# DeepSeek-R1

## Reinforcement Learning for Reasoning

**DeepSeek-R1**, released in January 2025, is a reasoning-model family based on DeepSeek-V3-Base. The full models have **671B total parameters**, activate about **37B per token**, and support a **128K context window**.

## DeepSeek-R1-Zero

R1-Zero tested whether reasoning behavior could emerge by applying large-scale reinforcement learning directly to a base model, without supervised fine-tuning first.

```text
Problem → Generated reasoning and answer → Verifiable reward → RL update
```

Long reasoning, reflection, and self-verification emerged during training. However, R1-Zero also suffered from repetition, poor readability, and language mixing.

## DeepSeek-R1

The main R1 pipeline addressed those weaknesses with cold-start supervised data, reasoning-focused RL, rejection sampling, further supervised fine-tuning, and a final RL stage for helpfulness and harmlessness.

It is important not to equate visible reasoning text with guaranteed correctness. A long chain of thought may still contain an early error that affects the final answer.

## Distilled Models

DeepSeek used outputs from R1 to fine-tune smaller dense Qwen and Llama models:

| Family | Sizes |
|---|---|
| R1-Distill-Qwen | 1.5B, 7B, 14B, 32B |
| R1-Distill-Llama | 8B, 70B |

These are not compressed copies of the 671B architecture. They are separate base models trained on reasoning examples produced by R1.

## Why It Mattered

R1 provided an open demonstration that verifiable rewards and large-scale RL can elicit strong reasoning behavior, and that the resulting behavior can be transferred into smaller models through distillation.

## Limitations

- Reasoning can be verbose, inefficient, or incorrect.
- Strong benchmark performance does not guarantee factual reliability.
- Distilled models do not have all capabilities of full R1.
- Outputs still need verification in mathematical, coding, medical, legal, or financial settings.

## Source

- [Official DeepSeek-R1 repository and paper](https://github.com/deepseek-ai/DeepSeek-R1)
