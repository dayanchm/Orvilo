# DeepSeek-V3.1

## One Model with Thinking and Non-Thinking Modes

**DeepSeek-V3.1**, released in 2025, is a hybrid model that can operate in two modes through its chat template:

```text
Non-thinking mode → faster direct response
Thinking mode     → explicit reasoning before the final response
```

This combined behavior that previously required choosing between a general V3 model and an R1-style reasoning model.

## Model Scale

| Property | Value |
|---|---:|
| Total parameters | 671B |
| Active parameters per token | 37B |
| Context length | 128K |

The architecture remains in the V3 family, using DeepSeekMoE and Multi-head Latent Attention.

## Longer-Context Training

V3.1-Base was built from the original V3 Base checkpoint using a two-stage context extension. DeepSeek substantially expanded training at both 32K and 128K lengths so the model could work more effectively with long documents.

## Tool Use and Agents

Post-training improved function calling, tool selection, and multi-step agent tasks. A model used as an agent must do more than answer once:

```text
Understand goal → choose tool → interpret result → continue or finish
```

V3.1's hybrid modes let applications choose speed or deeper reasoning without loading a different checkpoint.

## Why It Mattered

V3.1 shifted the DeepSeek line from separate “chat” and “reasoning” identities toward a single controllable model. It also strengthened the tool-use foundation developed further in V3.2.

## Limitations

Thinking mode costs more tokens and latency and does not guarantee correctness. Tool calls require validation, permission controls, and error handling. The full model also remains expensive to self-host.

## Source

- [Official DeepSeek-V3.1 model card](https://huggingface.co/deepseek-ai/DeepSeek-V3.1)
