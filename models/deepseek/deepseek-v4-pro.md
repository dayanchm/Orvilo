# DeepSeek-V4-Pro

## The High-Capacity V4 Variant

**DeepSeek-V4-Pro**, released in 2026, is the largest member of the original V4 family.

| Property | Value |
|---|---:|
| Total parameters | 1.6T |
| Active per token | 49B |
| Context window | 1M tokens |

Despite having 1.6 trillion total parameters, MoE routing activates only a subset for each token. Pro is designed for difficult reasoning, software engineering, tool use, and long-running agent tasks where capability is prioritized over serving cost.

The instruction model supports non-thinking, Think High, and Think Max modes. Think Max spends the most inference computation and requires a sufficiently large context allocation.

Pro's large total weights still demand substantial distributed storage and compute. A million-token input can also create major attention, cache, latency, and cost pressure. Applications must validate tool calls and generated code rather than treating model confidence as correctness.

## Source

- [Official DeepSeek-V4 model card](https://fe-static.deepseek.com/chat/transparency/deepseek-V4-model-card-EN.pdf)
