# Fine-Tuning

Fine-tuning continues training a pretrained model on a smaller, targeted dataset. It adapts behavior, domain performance, formatting, or task skill without repeating pretraining from scratch.

## Fine-Tuning Families

~~~mermaid
flowchart TD
    B["Pretrained model"] --> FT["Fine-tuning"]
    FT --> C["Continued pretraining"]
    FT --> S["Supervised fine-tuning"]
    FT --> P["Preference optimization"]
    FT --> RL["Reinforcement learning"]
    S --> FF["Full-parameter"]
    S --> PEFT["Parameter-efficient"]
~~~

The term is broad. Always specify the objective and data rather than saying only “fine-tuned.”

## Full and Parameter-Efficient Methods

| Method | Trainable parameters | Strength | Limitation |
|---|---:|---|---|
| Full fine-tuning | All | Maximum flexibility | High memory and storage |
| Adapter layers | Small added modules | Modular | Runtime architecture changes |
| LoRA | Low-rank weight updates | Efficient and widely supported | Rank limits update capacity |
| Prefix or prompt tuning | Learned virtual tokens | Very small footprint | Can trail weight adaptation |
| BitFit | Bias parameters | Extremely small | Limited capability |
| Quantized LoRA | Low-rank adapters over quantized base | Low hardware requirement | Quantization and merge details |

Parameter efficiency does not automatically mean data efficiency or equal final quality.

## LoRA Intuition

For a frozen weight matrix W, LoRA learns a low-rank update:

~~~text
W_effective = W + A × B
~~~

A and B contain far fewer parameters than W. Adapters can be stored separately or merged when deployment supports it.

## Dataset Design

Examples should reflect real inputs, desired outputs, edge cases, refusals, and formatting. A thousand high-quality, diverse examples can be more useful than a much larger noisy set.

Split by source or scenario to avoid nearly identical examples across train and evaluation.

## Hyperparameters

Important choices include learning rate, epochs, batch size, sequence length, packing, loss mask, warmup, weight decay, adapter rank, dropout, and precision.

Overtraining can make responses repetitive, reduce general skills, or memorize examples. Monitor held-out performance throughout training.

## Fine-Tuning Is Not a Knowledge Database

Fine-tuning may teach recurring domain patterns, but it is difficult to update or cite individual facts in weights. Use RAG or structured tools for changing, private, or auditable knowledge.

## Deployment

Pin the base-model revision, tokenizer, chat template, adapter, quantization, and inference runtime. Test the exact deployed combination; a correct adapter on the wrong base model can silently fail.

## Evaluation

Compare against the untuned baseline. Measure target-task quality, general-capability regressions, safety, calibration, latency, and data memorization.

## Related Guides

- [Pretraining](pretraining.md)
- [Instruction Tuning](instruction-tuning.md)
- [Supervised Fine-Tuning](supervised-fine-tuning.md)
