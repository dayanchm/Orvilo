# Gemini 1.5

## The Long-Context Generation

**Gemini 1.5**, introduced in February 2024, made long-context understanding the defining feature of the Gemini family. Its production models supported context windows of up to **1 million tokens**, while research tests reached 10 million tokens.

## Model Variants

- **Gemini 1.5 Pro** balanced capability with broad multimodal use.
- **Gemini 1.5 Flash** prioritized speed, high throughput, and lower cost.
- **Gemini 1.5 Flash-8B** targeted lighter, high-volume workloads.

## Mixture-of-Experts Architecture

Gemini 1.5 used a **Mixture-of-Experts (MoE)** architecture. Instead of sending every token through the full model, a routing mechanism selects relevant expert networks.

```text
Input token → Router → Selected experts → Combined output
```

This increases model capacity while controlling the computation used for each token.

## What Long Context Enables

A one-million-token prompt can contain large codebases, many documents, long videos, or hours of audio.

```text
Documents + images + audio + video + code
                     ↓
             One shared context
                     ↓
          Search, compare, and answer
```

This differs from retrieval systems that first select a few external passages. Gemini can directly receive a large body of material, although retrieval may still reduce cost and noise.

## Why It Mattered

Gemini 1.5 turned context length into a central model capability and introduced the enduring Pro/Flash distinction: Pro for harder tasks and Flash for efficient, high-volume use.

## Limitations

Maximum context is not the same as perfect recall. Relevant details can be missed, long prompts cost more to process, and multimodal reasoning can still produce unsupported conclusions.

## Sources

- [Gemini 1.5 technical report](https://arxiv.org/abs/2403.05530)
- [Google explanation of the long context window](https://blog.google/innovation-and-ai/products/long-context-window-ai-models/)
