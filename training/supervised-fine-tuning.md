# Supervised Fine-Tuning

Supervised fine-tuning (**SFT**) trains a model on examples of desired input–output behavior. For assistants, these are usually conversations whose assistant messages serve as targets.

Instruction tuning describes the behavioral goal; SFT is the optimization method commonly used to achieve it.

## SFT Step

~~~mermaid
flowchart LR
    E["Conversation example"] --> T["Apply chat template"]
    T --> M["Mask non-target tokens"]
    M --> F["Forward pass"]
    F --> CE["Cross-entropy loss"]
    CE --> B["Backpropagation"]
    B --> U["Update weights or adapter"]
~~~

## Example

~~~text
System: Answer from the supplied policy.
User: How many leave days may carry over?
Assistant: Up to five unused days may carry over.
~~~

The prompt tokens provide context. Loss can be computed only for the assistant response.

## Dataset Quality

High-quality SFT data should be correct, relevant, diverse, well formatted, policy compliant, and representative of production inputs.

Store provenance, annotator or generator information, review status, language, task category, and version. Resolve conflicting examples before training.

## Single-Turn and Multi-Turn Data

Single-turn examples efficiently teach broad tasks. Multi-turn conversations teach reference resolution, clarification, correction, and consistent state.

Long synthetic conversations can drift or contain contradictions. Review entire trajectories, not isolated messages.

## Sampling

Large categories can dominate training even when product importance is low. Balance tasks deliberately, and consider temperature-based or capped sampling.

Mixing safety refusals too heavily can cause over-refusal; too lightly can leave unsafe gaps.

## Training Choices

- full-parameter or parameter-efficient update;
- learning rate and scheduler;
- effective batch size;
- number of epochs;
- maximum sequence length;
- packing strategy;
- loss mask;
- example weights;
- checkpoint selection.

SFT learning rates are generally much lower than pretraining rates because the goal is adaptation without destroying existing capabilities.

## Common Failure Modes

- memorizing a small dataset;
- learning annotation artifacts;
- copying verbose teacher style;
- format corruption from a mismatched chat template;
- catastrophic forgetting;
- weak performance on prompts unlike the demonstrations;
- unsafe compliance or excessive refusal.

## Evaluation

Compare several checkpoints, not only the final one. Evaluate target tasks, general benchmarks, safety, memorization, calibration, style, and exact structured-output validity.

SFT produces a useful initial policy for later preference optimization or reinforcement learning.

## Related Guides

- [Instruction Tuning](instruction-tuning.md)
- [RLHF](rlhf.md)
- [Fine-Tuning](fine-tuning.md)
