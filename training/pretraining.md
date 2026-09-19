# Pretraining

Pretraining teaches a model broad statistical patterns from large datasets before it is adapted for conversation or specialized tasks.

For decoder-only language models, the dominant objective is causal next-token prediction.

## Causal Language Modeling

~~~text
Input:  The policy grants twenty
Target: policy grants twenty days
~~~

At each position, causal attention prevents the model from seeing future target tokens. Predicting billions or trillions of tokens teaches syntax, facts, code patterns, and reusable representations.

## Pretraining Pipeline

~~~mermaid
flowchart LR
    D["Versioned data mixture"] --> T["Tokenizer"]
    T --> SH["Packed training shards"]
    SH --> TR["Distributed training"]
    TR --> CK["Checkpoints"]
    CK --> EV["Validation + evaluations"]
    EV -- "continue" --> TR
    EV -- "select" --> M["Base model"]
~~~

## Base Models

A pretrained base model continues text; it has not necessarily learned to interpret chat roles or reliably follow user instructions. Post-training transforms this completion behavior into assistant behavior.

Base models remain valuable for research, continued pretraining, and specialized adaptation.

## Data and Compute Balance

Model size, dataset size, and compute should be balanced. A very large model trained on too few tokens may be undertrained; a smaller model trained on more high-quality data can be more efficient.

Scaling laws describe average relationships, not guarantees for every architecture or data mixture.

## Training Schedule

A typical run includes:

- learning-rate warmup;
- a peak learning rate;
- decay over the remaining tokens;
- periodic validation;
- checkpointing model and optimizer state;
- data-mixture or curriculum phases;
- final annealing on higher-quality data.

Changing the data mixture late in training can substantially affect final behavior.

## Packing and Attention

Packing places multiple documents into one fixed-length training sequence to reduce padding. Attention masks and boundary handling must prevent unwanted leakage when documents should remain independent.

Long-context training costs more because standard attention grows approximately quadratically with sequence length. Many models first train on shorter sequences and later extend context.

## Continued Pretraining

Continued pretraining adapts a base model to a domain, language, or longer context using the original or a related language-model objective. It can add terminology and style, but may cause catastrophic forgetting if the mixture is too narrow.

Mix general data, lower the learning rate, and evaluate both domain gains and broad capabilities.

## Checkpoints

A full training checkpoint can include weights, optimizer moments, scheduler state, random-number state, and data-loader position. Weight-only checkpoints are smaller but cannot resume training exactly.

Test restoration before a long run depends on it.

## Evaluation and Safety

Track validation loss, downstream tasks, memorization, contamination, bias, dangerous capabilities, and data-regime performance. Pretraining data may contain personal information, insecure code, harmful instructions, and false claims.

## Further Reading

- [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361)
- [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556)
