# Alignment

Alignment is the effort to make model behavior better reflect human intentions, values, policies, and legitimate user goals. It is not one algorithm or a state that can be declared complete.

## Alignment Stack

~~~mermaid
flowchart TD
    P["Pretrained capabilities"] --> S["Supervised demonstrations"]
    S --> PF["Preference feedback"]
    PF --> RL["Preference optimization / RL"]
    RL --> SP["System policies and safeguards"]
    SP --> EV["Evaluation and monitoring"]
    EV -- "new failures" --> S
~~~

Training is only one layer. Product permissions, input and output controls, monitoring, incident response, and human oversight remain necessary.

## What Is Being Aligned?

| Dimension | Desired behavior |
|---|---|
| Helpfulness | Understand and advance legitimate goals |
| Honesty | Express uncertainty and avoid fabricated claims |
| Harmlessness | Avoid enabling serious harm |
| Instruction hierarchy | Respect higher-priority instructions |
| Steerability | Follow requested style and constraints |
| Corrigibility | Accept correction and oversight |
| Fairness | Avoid unjustified differential treatment |
| Agency | Avoid unauthorized or irreversible actions |

These goals can conflict. A useful system needs explicit policies and escalation paths.

## Alignment Methods

- supervised examples of desired behavior;
- human or AI preference comparisons;
- direct preference optimization;
- reinforcement learning from learned or verifiable rewards;
- constitutional or principle-based feedback;
- red teaming and adversarial training;
- runtime classifiers and permission systems.

No method guarantees behavior outside its evaluation distribution.

## Outer and Inner Alignment

**Outer alignment** asks whether the specified objective captures what people want. **Inner alignment** asks whether the trained model actually pursues the intended objective, including in new situations.

A reward model can be optimized while missing the real goal. This is one form of specification gaming.

## Helpful Refusal

A good model refuses only the unsafe portion, explains the boundary without exposing harmful detail, and offers safe alternatives. Over-refusal harms legitimate users; under-refusal creates risk.

Measure both types of error across languages and domains.

## Agents and Alignment

Tool-using models can produce real-world side effects. Training should not be treated as authorization. Enforce least privilege, approval gates, sandboxing, transaction limits, and audit logs in software.

Prompt injection from documents or websites is an application-security problem as well as a model-behavior problem.

## Evaluation

Use capability tests, policy tests, jailbreaks, distribution shifts, long conversations, deceptive-context scenarios, agent simulations, and expert red teams.

Report uncertainty and limitations. A model can pass a benchmark while failing a semantically equivalent prompt.

## Governance

Document objectives, data, annotator guidance, policy changes, evaluation thresholds, deployment decisions, and incidents. High-stakes changes require independent review and rollback capability.

## Further Reading

- [Constitutional AI](https://arxiv.org/abs/2212.08073)
- [Learning from Human Preferences](https://arxiv.org/abs/1706.03741)
- [InstructGPT](https://arxiv.org/abs/2203.02155)
