# GPT-1

**GPT-1** was introduced in 2018 in *Improving Language Understanding by Generative Pre-Training*. It showed that one decoder-only Transformer could learn from unlabeled text and then be fine-tuned for many NLP tasks.

## Key Facts

- 117 million parameters and 12 Transformer layers
- Left-to-right autoregressive next-token prediction
- Pretrained on BooksCorpus, then fine-tuned with labeled task data
- 512-token input length

GPT-1 established the two-stage pattern:

```text
General pretraining → Task-specific fine-tuning
```

Its importance was methodological rather than conversational: it demonstrated reusable representations, but still required separate adaptation for most tasks.

## Source

- [Original GPT paper](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)
