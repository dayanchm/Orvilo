# Llama 4

**Llama 4**, released in 2025, moved the main Llama line from dense models to natively multimodal **Mixture-of-Experts (MoE)** models.

| Model | Total parameters | Active parameters | Context |
|---|---:|---:|---:|
| Llama 4 Scout | 109B | 17B | 10M |
| Llama 4 Maverick | 400B | 17B | 1M |

Both accept text and images. MoE routing activates only a subset of experts per token, increasing capacity without using every parameter on every step. Scout emphasizes extreme context and deployability; Maverick emphasizes capability.

Long context does not guarantee perfect recall, and multimodal outputs still require verification.

## Source
- [Meta Llama repository](https://github.com/meta-llama/llama-models)
