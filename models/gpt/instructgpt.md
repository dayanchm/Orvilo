# InstructGPT

**InstructGPT**, introduced in 2022, adapted GPT-3 models to follow user intentions more reliably using human feedback.

## Training Pipeline

```text
Human demonstrations → Supervised fine-tuning
Ranked model answers → Reward model
Reward signal → Reinforcement learning from human feedback
```

This process is commonly called **RLHF**. Labelers demonstrated desired behavior and ranked candidate responses; a reward model learned those preferences, and reinforcement learning optimized the assistant.

InstructGPT showed that alignment training can matter more to perceived usefulness than parameter count: smaller aligned models were often preferred to the much larger base GPT-3. It directly influenced the assistant-style behavior later associated with ChatGPT.

RLHF does not guarantee truth or safety. Human preferences can be incomplete, inconsistent, or biased, and a helpful-sounding answer can still be wrong.

## Source

- [Training language models to follow instructions](https://arxiv.org/abs/2203.02155)
