# DeepSeek-V3.2-Speciale

## A High-Compute Reasoning Variant

**DeepSeek-V3.2-Speciale** is a variant of V3.2 optimized for especially difficult reasoning problems. It uses the same broad model structure and sparse-attention foundation, but allocates more inference computation to producing and checking a solution.

```text
More reasoning computation → longer deliberation → potentially stronger solution
```

Its focus includes competition mathematics and programming. DeepSeek reported gold-medal-level results on 2025 International Mathematical Olympiad and International Olympiad in Informatics evaluations, but benchmark results should not be treated as proof of universal reliability.

Unlike standard V3.2, **Speciale does not support tool calling**. It is intended for self-contained deep reasoning rather than interactive agent workflows.

Use it when solution quality matters more than speed or token cost. Standard V3.2 is the more appropriate variant when tools, agents, or lower latency are required.

## Source

- [Official DeepSeek-V3.2 model card](https://huggingface.co/deepseek-ai/DeepSeek-V3.2)
