# Reinforcement Learning for Language Models

Reinforcement learning (**RL**) optimizes a policy from rewards rather than only imitating target text. For language models, the policy selects tokens or actions and receives a score for the resulting response or trajectory.

## RL Loop

~~~mermaid
flowchart LR
    T["Task"] --> P["Policy model"]
    P --> A["Response or actions"]
    A --> E["Environment / evaluator"]
    E --> R["Reward"]
    R --> U["Policy update"]
    U --> P
~~~

For agentic tasks, the trajectory may include tool calls and observations before a final reward.

## Key Terms

| Term | Meaning |
|---|---|
| State | Information available before an action |
| Action | A token, tool call, or decision |
| Policy | Distribution over possible actions |
| Trajectory | Sequence of states, actions, and rewards |
| Reward | Numeric training signal |
| Return | Accumulated future reward |
| Value function | Expected return from a state |
| Advantage | How much better an action was than expected |

## Reward Sources

- human preferences;
- learned reward models;
- automatically checked math answers;
- unit tests for generated code;
- compiler or theorem-prover feedback;
- game or simulator outcomes;
- policy and safety classifiers;
- task-completion evidence.

Verifiable rewards scale well when correctness can be checked automatically. A passing weak test suite is not proof of correct code.

## Online and Offline Learning

Online RL generates new trajectories with the current policy. It adapts to changing behavior but is computationally expensive.

Offline methods learn from a fixed dataset of demonstrations or preferences. They are simpler operationally but cannot explore new behavior during training.

## Credit Assignment

A final outcome may depend on many earlier tokens or actions. Credit assignment determines which decisions should be reinforced.

Process supervision adds intermediate feedback, while outcome supervision judges only the final result. Intermediate labels can guide reasoning but are costly and may enforce one preferred path.

## Exploration and Diversity

A deterministic policy cannot discover alternatives. Sampling temperature and multiple candidates support exploration, but unconstrained exploration can produce unsafe or low-quality trajectories.

Run training environments with strict tool permissions and isolated resources.

## Stability

Policy optimization can collapse output diversity, exploit the reward, or damage language quality. Common controls include KL penalties, clipped updates, reference policies, reward normalization, advantage estimation, and conservative learning rates.

Monitor reward alongside independent task and safety evaluations.

## Agentic RL

For tool-using agents, define explicit success, step limits, tool costs, and penalties for invalid or unnecessary actions. Avoid rewarding mere activity.

The training sandbox must not expose real credentials, production systems, or unrestricted network access.

## Evaluation

Measure verified success, reward–quality correlation, trajectory efficiency, generalization, safety, diversity, and robustness to evaluator changes. Compare with SFT and best-of-N baselines before accepting RL complexity.

## Related Guides

- [RLHF](rlhf.md)
- [Alignment](alignment.md)
- [Supervised Fine-Tuning](supervised-fine-tuning.md)
