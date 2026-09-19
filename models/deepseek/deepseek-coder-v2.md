# DeepSeek-Coder-V2

## Code Intelligence Built on DeepSeek-V2

**DeepSeek-Coder-V2**, released in 2024, is an MoE code-model family created by continuing the pretraining of an intermediate DeepSeek-V2 checkpoint on an additional **6 trillion tokens**.

| Version | Total parameters | Active per token | Context |
|---|---:|---:|---:|
| Coder-V2-Lite | 16B | 2.4B | 128K |
| Coder-V2 | 236B | 21B | 128K |

Both were released as Base and Instruct checkpoints.

## What Changed from DeepSeek Coder

```text
Languages:       86 → 338
Context window: 16K → 128K
Architecture: dense models → DeepSeekMoE + MLA
```

The larger context window makes it possible to reason over more files, long specifications, build output, and repository-level dependencies.

## Architecture

Coder-V2 inherits two ideas from DeepSeek-V2:

- **DeepSeekMoE** routes each token through a subset of experts.
- **MLA** compresses attention state to reduce the KV-cache cost.

It also retains code completion and fill-in-the-middle behavior.

## General and Mathematical Ability

Although code is its specialization, continued training was designed to improve mathematical reasoning while preserving general-language ability. This is useful because real programming combines source code with issue descriptions, documentation, formulas, and tool output.

## Limitations

- A 128K limit does not guarantee that every detail in a long repository will be used correctly.
- Generated programs may compile yet remain logically wrong or insecure.
- Package names and APIs may be hallucinated or outdated.
- The full 236B checkpoint requires demanding inference infrastructure.

## Why It Mattered

Coder-V2 connected DeepSeek's specialist coding line with its efficient general-model architecture. Its code abilities were later merged with general chat behavior in DeepSeek-V2.5.

## Source

- [Official DeepSeek-Coder-V2 repository](https://github.com/deepseek-ai/DeepSeek-Coder-V2)
