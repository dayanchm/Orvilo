# Reinforcement Learning from Human Feedback

Reinforcement Learning from Human Feedback (**RLHF**) uses human judgments about model outputs to train a preference signal and improve a language-model policy.

The term often describes a pipeline of supervised fine-tuning, preference collection, reward modeling, and reinforcement learning.

## Classic RLHF Pipeline

~~~mermaid
flowchart LR
    B["Base model"] --> S["SFT"]
    S --> C["Generate candidates"]
    C --> H["Human rankings"]
    H --> RM["Train reward model"]
    S --> RL["RL policy optimization"]
    RM --> RL
    REF["Reference model"] --> RL
    RL --> A["Aligned model"]
~~~

## Preference Data

Annotators compare responses to the same prompt according to a rubric such as correctness, helpfulness, safety, and style.

A comparison record can contain the prompt, chosen response, rejected response, annotator metadata, disagreement, policy version, and task category.

Preferences are not universal truth. They reflect instructions, annotator populations, cultural context, and sampling choices.

## Reward Models

A reward model assigns a scalar score to a prompt–response pair. It is trained so the chosen response scores above the rejected response.

~~~text
P(chosen preferred) =
    sigmoid(reward_chosen - reward_rejected)
~~~

Reward-model accuracy on held-out comparisons does not guarantee reliable scores for very different responses.

## Policy Optimization

PPO is a classic RLHF method. It increases expected reward while constraining updates so the policy does not move too far from a reference model. A KL penalty helps preserve capabilities and language quality.

Alternative preference methods such as DPO optimize comparison data directly without separately running online RL against a reward model.

## Reward Hacking

A policy may exploit weaknesses in the reward model: excessive verbosity, confident phrasing, unnecessary headings, copied rubric language, or other superficial features can receive high scores without better answers.

Maintain independent evaluations that the policy cannot directly optimize.

## Human Factors

Provide clear rubrics, training, calibration examples, escalation, fair compensation, and support for disturbing content. Measure inter-annotator agreement and preserve disagreement rather than forcing arbitrary consensus.

Protect annotator privacy and separate personally identifying information from training records.

## Evaluation

Measure task success, factuality, preference win rate, reward margin, KL divergence, diversity, calibration, refusal quality, and capability regressions.

Use red teams and out-of-distribution tests to detect reward exploitation.

## Limitations

RLHF can improve average behavior without solving hallucination, bias, sycophancy, or adversarial robustness. Human feedback is expensive and may miss rare but severe failures.

## Further Reading

- [Learning to Summarize from Human Feedback](https://arxiv.org/abs/2009.01325)
- [InstructGPT](https://arxiv.org/abs/2203.02155)
- [Direct Preference Optimization](https://arxiv.org/abs/2305.18290)
