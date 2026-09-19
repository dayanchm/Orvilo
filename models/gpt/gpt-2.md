# GPT-2

**GPT-2**, released in 2019, scaled the decoder-only GPT architecture to 1.5 billion parameters and trained it on WebText, a diverse corpus collected from about eight million web pages.

## Main Idea

GPT-2 framed tasks as text completion. Translation, summarization, and question answering could sometimes emerge without task-specific parameter updates.

```text
Prompt describing a task → Next-token prediction → Task-like completion
```

The largest model used 48 layers and a 1,024-token context. It also introduced byte-level BPE tokenization to the GPT line. Its fluent long-form generation prompted a staged release and an early public discussion about model misuse.

GPT-2 could be coherent and versatile, but also repetitive, factually wrong, biased, and sensitive to prompt wording.

## Source

- [Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)
