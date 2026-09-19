# DeepSeek-V4

## Long-Context Models for Agentic Work

**DeepSeek-V4**, released in April 2026, is a Mixture-of-Experts model family designed around very long context and multi-step agent workloads.

| Model | Total parameters | Active per token | Context |
|---|---:|---:|---:|
| DeepSeek-V4-Flash | 284B | 13B | 1M tokens |
| DeepSeek-V4-Pro | 1.6T | 49B | 1M tokens |

Base and instruction-tuned checkpoints were released for both sizes. Flash prioritizes efficiency, while Pro provides greater capacity.

## Why a Million-Token Context Matters

Long-running agents can accumulate source files, documents, tool results, and earlier decisions. A larger context window delays the need to discard or summarize that history.

```text
User goal
  + repository or documents
  + many tool interactions
  + intermediate decisions
  → one continuing agent trajectory
```

A maximum window is a capacity limit, not a promise of perfect recall. Relevant evidence can still be overlooked in a very long prompt.

## Reasoning Modes

The instruction models support three operating styles:

- **Non-think** for fast direct answers
- **Think High** for explicit reasoning
- **Think Max** for the most compute-intensive reasoning

This exposes a practical tradeoff between latency, token use, and problem-solving effort.

## Architecture and Precision

V4 continues the MoE approach: only a subset of parameters is activated for each token. Released instruction checkpoints use mixed low precision, with FP4 expert weights and mostly FP8 elsewhere, to reduce the enormous storage and bandwidth requirements.

## Agent Focus

V4 post-training emphasizes tool use, software engineering, and long multi-step tasks. Effective deployment still needs an external agent harness to define tools, validate arguments, enforce permissions, manage failures, and decide when work is complete.

## Limitations

- One million tokens can still be expensive to process and store in a KV cache.
- Long context does not ensure that the model uses every detail correctly.
- Tool-using models can take harmful actions if applications omit permission boundaries.
- Even Flash is a very large model; Pro requires substantial distributed infrastructure.
- Generated claims, reasoning, and code still require verification.

## Sources

- [Official DeepSeek model overview](https://www.deepseek.com/en/transparency/)
- [DeepSeek-V4 model card](https://fe-static.deepseek.com/chat/transparency/deepseek-V4-model-card-EN.pdf)
