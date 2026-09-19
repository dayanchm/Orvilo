# GPT-3

**GPT-3**, introduced in 2020, scaled autoregressive language modeling to 175 billion parameters. Its central result was **in-context learning**: tasks could be specified with instructions and examples inside the prompt, without updating model weights.

## Evaluation Settings

- **Zero-shot:** instruction only
- **One-shot:** one demonstration
- **Few-shot:** several demonstrations

```text
Instruction + examples + new input → Completion
```

The largest model used 96 layers and a 2,048-token context. It was trained on a mixture including filtered Common Crawl, WebText-style data, books, and Wikipedia.

GPT-3 made prompting a practical interface, but remained sensitive to wording and could hallucinate, reproduce biases, and fail at exact reasoning.

## Source

- [Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165)
