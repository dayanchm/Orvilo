# Knowledge Distillation

Knowledge distillation transfers useful behavior from a teacher model or ensemble into a student model. The student is usually smaller, faster, or cheaper to deploy.

## Distillation Pipeline

~~~mermaid
flowchart LR
    X["Training inputs"] --> T["Teacher"]
    X --> S["Student"]
    T --> Y["Teacher signal"]
    Y --> L["Distillation loss"]
    S --> L
    G["Ground-truth targets"] --> L
    L --> U["Update student"]
~~~

## Distillation Signals

| Signal | Description |
|---|---|
| Hard labels | Teacher's selected answer or token |
| Soft logits | Full probability distribution over tokens |
| Hidden states | Intermediate teacher representations |
| Attention maps | Teacher attention patterns |
| Generated rationales | Explanations or solution traces |
| Tool trajectories | Actions, observations, and final result |
| Preference pairs | Teacher-selected better and worse outputs |

API-only teachers generally expose generated outputs, not logits or hidden states.

## Soft Targets

A probability distribution reveals alternatives that a hard target hides. Temperature can soften logits:

~~~text
teacher_probs = softmax(teacher_logits / temperature)
~~~

The student's objective may combine ground-truth cross-entropy with divergence from the teacher distribution.

## Sequence-Level Distillation

The teacher generates responses for an instruction dataset and the student learns from them through SFT. This is simple and scalable but transfers teacher mistakes, style, and biases.

Filter and verify outputs. For code and mathematics, execution-based checks are stronger than fluency judgments.

## Reasoning Distillation

Teacher-generated reasoning traces can help students solve multi-step tasks, but visible explanations are not guaranteed to reflect the teacher's actual computation. Long traces can also waste tokens or contain hidden errors.

Train and evaluate final correctness separately from explanation quality.

## Student Capacity

A student cannot necessarily represent every teacher behavior. Select important domains, compress response style, and match task difficulty to capacity.

A well-trained smaller student may outperform its teacher on a narrow distribution while remaining weaker broadly.

## Legal and Policy Considerations

Confirm that teacher terms permit the intended generation and training use. Track provenance, licenses, private inputs, and restrictions on model extraction.

Do not assume publicly accessible outputs are unrestricted training material.

## Evaluation

Compare student with teacher and original baseline on quality, latency, throughput, memory, cost, calibration, safety, and out-of-domain tasks.

Measure compression benefit end to end. A slightly smaller model that requires more retries may not reduce product cost.

## Distillation Versus Quantization

Distillation trains a new model. Quantization stores or computes existing weights at lower precision. They can be combined but introduce different errors.

## Further Reading

- [Distilling the Knowledge in a Neural Network](https://arxiv.org/abs/1503.02531)
- [DistilBERT](https://arxiv.org/abs/1910.01108)
