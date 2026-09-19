# Synthetic Training Data

Synthetic data is generated or transformed by models, programs, simulators, or rules rather than collected directly from naturally occurring examples. It can expand coverage, target weaknesses, and provide scalable supervision.

## Generation Pipeline

~~~mermaid
flowchart LR
    N["Training need"] --> G["Generate candidates"]
    G --> F["Filter"]
    F --> V["Verify"]
    V --> D["Deduplicate"]
    D --> M["Mix with real data"]
    M --> T["Train"]
    T --> E["Evaluate"]
    E -- "new gaps" --> N
~~~

## Common Uses

| Technique | Example |
|---|---|
| Self-instruction | Generate new tasks and responses |
| Rewriting | Improve clarity or vary style |
| Translation | Expand multilingual coverage |
| Simulation | Create tool-use or dialogue trajectories |
| Counterfactuals | Change attributes while preserving labels |
| Hard-negative mining | Generate plausible wrong alternatives |
| Distillation | Use a stronger teacher's outputs |
| Verifiable generation | Produce math or code checked automatically |

## Quality Control

Use deterministic validators where possible: compilers, tests, calculators, schemas, database checks, and exact simulators. Model judges are useful but can share the generator's blind spots.

A layered filter may check policy, language, duplicates, answer correctness, difficulty, diversity, and similarity to evaluation data.

## Diversity

Prompt templates can create millions of examples that differ only superficially. Measure semantic diversity, topic distribution, reasoning pattern, length, language, and source concentration.

Use multiple generation methods or teachers when appropriate, but do not assume model variety guarantees independent errors.

## Model Collapse and Error Amplification

Repeatedly training on generated text can narrow the distribution and amplify inaccuracies or stylistic artifacts. Preserve high-quality real data, track synthetic proportions, and evaluate rare cases.

Generated examples should never be labeled as human-authored.

## Contamination

A teacher may reproduce benchmark questions, copyrighted passages, personal information, or secrets from its context. Compare synthetic data against protected evaluation sets and run privacy and provenance checks.

Do not use production user data as generation context without appropriate consent and controls.

## Curriculum and Difficulty

Generate examples at several difficulty levels. If every synthetic task is easy for the teacher, the student gains little. If examples are unverifiable and too hard, error rates rise.

Adaptive pipelines can target failures found during evaluation, while holding out separate tests to avoid optimizing directly against them.

## Documentation

Record generator model and version, prompt, sampling settings, source context, filters, validators, timestamps, licenses, and review status. This enables removal and reproducibility.

## Evaluation

Compare real-only, synthetic-only, and mixed training runs. Measure target gains, generalization, calibration, bias, safety, memorization, and performance outside the teacher's preferred style.

## Related Guides

- [Datasets](datasets.md)
- [Distillation](distillation.md)
- [Instruction Tuning](instruction-tuning.md)
