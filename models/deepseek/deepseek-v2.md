# DeepSeek-V2

## An Efficient Mixture-of-Experts Language Model

**DeepSeek-V2**, released in 2024, replaced the earlier dense design with a **Mixture-of-Experts (MoE)** architecture and introduced **Multi-head Latent Attention (MLA)**.

| Version | Total parameters | Active per token | Context |
|---|---:|---:|---:|
| DeepSeek-V2-Lite | 16B | 2.4B | 32K |
| DeepSeek-V2 | 236B | 21B | 128K |

## Mixture of Experts

A dense model uses nearly all of its parameters for every token. An MoE model contains many specialized feed-forward experts, while a router selects only a small subset for each token.

```text
Token → Router → Selected experts → Combined representation
```

DeepSeek-V2 therefore has 236B total parameters but activates about 21B for a token. This increases model capacity without paying the full computational cost on every step. DeepSeek calls its expert design **DeepSeekMoE**.

## Multi-head Latent Attention

Autoregressive generation normally stores attention keys and values for earlier tokens in a **KV cache**. That cache becomes expensive for long prompts.

MLA compresses key-value information into a smaller latent representation:

```text
Keys and values → Low-rank latent compression → Smaller KV cache
```

This makes long-context inference more memory-efficient. The official report states a 93.3% KV-cache reduction relative to its comparison baseline.

## Training

DeepSeek-V2 was pretrained on **8.1 trillion tokens**, then adapted with supervised fine-tuning and reinforcement learning. Base and Chat checkpoints were released.

## Why It Mattered

DeepSeek-V2 introduced the two architectural ideas—DeepSeekMoE and MLA—that became the backbone of later V3 and R1 models. It showed that total parameter count and per-token computation do not have to grow together.

## Limitations

MoE routing and MLA need specialized inference support. The full model is still extremely large to host, and efficiency does not remove ordinary language-model risks such as hallucination and bias.

## Source

- [Official DeepSeek-V2 repository and technical report](https://github.com/deepseek-ai/DeepSeek-V2)
