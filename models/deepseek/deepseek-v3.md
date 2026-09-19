# DeepSeek-V3

## Scaling the Efficient MoE Architecture

**DeepSeek-V3**, released in December 2024, is a large decoder-only Mixture-of-Experts model.

```text
671B total parameters
37B activated per token
61 Transformer layers
128K context window
14.8T pretraining tokens
```

## Architecture

V3 builds on DeepSeek-V2's **DeepSeekMoE** and **Multi-head Latent Attention**. It adds two notable training ideas.

### Auxiliary-Loss-Free Load Balancing

An MoE router must distribute tokens among experts. Traditional balancing losses can interfere with the main language objective. V3 uses a bias-based strategy to balance expert load without a separate auxiliary loss dominating training.

### Multi-Token Prediction

Ordinary language-model training predicts the next token. V3 also trains auxiliary modules to predict multiple future tokens:

```text
Current context → next token + later-token predictions
```

This supplies a denser training signal and can also support faster generation techniques such as speculative decoding.

## Training and Numerical Efficiency

DeepSeek-V3 was pretrained on 14.8 trillion tokens and then underwent supervised fine-tuning and reinforcement learning. Training used FP8 mixed precision extensively. DeepSeek reported 2.788 million H800 GPU hours for the complete training process.

The released weights include 671B main-model parameters plus a 14B multi-token-prediction module, which explains why some tools display approximately 685B parameters.

## Why It Mattered

V3 showed how MoE routing, compressed attention, lower-precision training, and multi-token prediction could scale an open-weight model while controlling per-token computation. Its Base checkpoint also became the architectural and training foundation for DeepSeek-R1.

## Limitations

Only a fraction of parameters activate per token, but all expert weights still require enormous storage and distributed hardware. V3 can hallucinate, inherit data biases, and fail at tasks needing verified facts or exact reasoning.

## Source

- [Official DeepSeek-V3 repository and technical report](https://github.com/deepseek-ai/DeepSeek-V3)
