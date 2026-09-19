# DeepSeek LLM

## The First General-Purpose DeepSeek Language Models

**DeepSeek LLM** is a family of autoregressive language models released in 2023. It established the general-language foundation that later DeepSeek models expanded.

The family contains four main checkpoints:

| Model | Purpose | Context length |
|---|---|---:|
| DeepSeek LLM 7B Base | Text completion and further training | 4,096 tokens |
| DeepSeek LLM 7B Chat | Conversation and instruction following | 4,096 tokens |
| DeepSeek LLM 67B Base | Larger foundation model | 4,096 tokens |
| DeepSeek LLM 67B Chat | Larger assistant model | 4,096 tokens |

## How It Works

DeepSeek LLM is a **decoder-only Transformer**. Like GPT-style models, it predicts each token from the tokens that came before it.

```text
Previous tokens → Transformer decoder → Next-token probabilities
```

The 7B model uses multi-head attention, while the 67B model uses grouped-query attention. Grouped-query attention lets multiple query heads share key/value heads, reducing inference memory use.

## Training

The base models were trained from scratch on **2 trillion tokens** of English and Chinese text with a sequence length of 4,096. The corpus was filtered and deduplicated to remove repeated and low-quality material.

The distinction between the checkpoints is important:

```text
Base model → general next-token predictor
Chat model → base model adapted to follow instructions and hold conversations
```

## Why It Mattered

DeepSeek LLM demonstrated DeepSeek's early focus on bilingual English-Chinese modeling, mathematics, coding, and openly available model weights. Later systems changed the architecture significantly, but retained the same autoregressive foundation.

## Limitations

- The 4K context window is small compared with later DeepSeek models.
- Base checkpoints are not assistants and may not follow instructions reliably.
- Chat checkpoints can hallucinate, reproduce training-data biases, and produce unsafe or incorrect answers.
- Running the 67B model locally requires substantial memory.

## Source

- [Official DeepSeek LLM repository](https://github.com/deepseek-ai/DeepSeek-LLM)
