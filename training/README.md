# Training Language Models

Training a language model is a pipeline that turns raw data into a model capable of predicting language, following instructions, and behaving safely in a target product.

This section explains both **pretraining**, where broad capabilities are learned from large corpora, and **post-training**, where behavior is adapted with demonstrations, preferences, feedback, and reinforcement learning.

## End-to-End Pipeline

~~~mermaid
flowchart LR
    D["Datasets"] --> T["Tokenization"]
    T --> P["Pretraining"]
    P --> S["Supervised<br/>fine-tuning"]
    S --> A["Alignment"]
    A --> E["Evaluation"]
    E --> DEP["Deployment"]
    E -- "Failures" --> D
    E -- "Behavior gaps" --> S
~~~

Training is iterative. Evaluation can reveal missing data, tokenizer problems, unsafe behavior, or weaknesses that require a different training stage.

## Learning Path

~~~mermaid
flowchart LR
    D["1. Datasets"] --> T["2. Tokenization"]
    T --> E["3. Embeddings"]
    E --> L["4. Loss functions"]
    L --> B["5. Backpropagation"]
    B --> P["6. Pretraining"]
    P --> F["7. Fine-tuning"]
    F --> I["8. Instruction tuning"]
    I --> S["9. SFT"]
    S --> A["10. Alignment"]
    A --> R["11. RLHF"]
    R --> RL["12. Reinforcement learning"]
    RL --> SD["13. Synthetic data"]
    SD --> K["14. Distillation"]

    click D "datasets.md"
    click T "tokenization.md"
    click E "embeddings.md"
    click L "loss-functions.md"
    click B "backpropagation.md"
    click P "pretraining.md"
    click F "fine-tuning.md"
    click I "instruction-tuning.md"
    click S "supervised-fine-tuning.md"
    click A "alignment.md"
    click R "rlhf.md"
    click RL "reinforcement-learning.md"
    click SD "synthetic-data.md"
    click K "distillation.md"
~~~

| Stage | Guide | What it explains |
|---:|---|---|
| 1 | [Datasets](datasets.md) | Collection, filtering, deduplication, mixtures, and governance |
| 2 | [Tokenization](tokenization.md) | How raw text becomes model input IDs |
| 3 | [Embeddings](embeddings.md) | How tokens become learned vectors |
| 4 | [Loss Functions](loss-functions.md) | What the optimization process minimizes |
| 5 | [Backpropagation](backpropagation.md) | How gradients update model parameters |
| 6 | [Pretraining](pretraining.md) | Learning general language capabilities |
| 7 | [Fine-Tuning](fine-tuning.md) | Adapting a pretrained model |
| 8 | [Instruction Tuning](instruction-tuning.md) | Learning to respond to user tasks |
| 9 | [Supervised Fine-Tuning](supervised-fine-tuning.md) | Training on curated input–response examples |
| 10 | [Alignment](alignment.md) | Shaping behavior around human intent and safety |
| 11 | [RLHF](rlhf.md) | Learning from human preference comparisons |
| 12 | [Reinforcement Learning](reinforcement-learning.md) | Optimizing behavior from rewards |
| 13 | [Synthetic Data](synthetic-data.md) | Creating scalable generated training examples |
| 14 | [Distillation](distillation.md) | Transferring capability into a smaller model |

## Training Phases Compared

| Phase | Starting point | Data | Main objective |
|---|---|---|---|
| Pretraining | Random or partially trained weights | Large unlabeled corpus | Predict tokens and learn representations |
| Continued pretraining | Pretrained model | Domain corpus | Learn domain language and knowledge |
| SFT | Pretrained model | Input–response demonstrations | Follow instructions |
| Preference optimization | SFT model | Ranked or labeled responses | Prefer desired behavior |
| Reinforcement learning | Post-trained model | Tasks plus verifiable or learned rewards | Improve multi-step behavior |
| Distillation | Student model | Teacher outputs or distributions | Preserve quality at lower cost |

## Core Principle

Training results reflect the combination of data, objective, model architecture, optimization, compute, and evaluation. Scaling only one dimension does not guarantee a better model.

Separate capability from product safety. A lower training loss does not prove factuality, fairness, robustness, or safe tool use.

## Further Reading

- [Attention Is All You Need](https://arxiv.org/abs/1706.03762)
- [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361)
- [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556)
