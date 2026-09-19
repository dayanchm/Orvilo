# Gemma 2

**Released:** June 2024

## Overview

Gemma 2 improved quality per parameter while keeping the family practical to host.

## Architecture and Training

The family includes 2B, 9B, and 27B variants. Google used knowledge distillation for smaller models and architectural techniques such as interleaved local and global attention, grouped-query attention, and logit soft-capping.

## Best Fit

It is suited to chat, summarization, extraction, and domain fine-tuning. The 9B model is a useful middle ground; deployment cost still depends on precision, batch size, and runtime.

## Limitations

Gemma 2 remains text-only and uses an 8K context window. Evaluate factuality and safety for the target domain.

## Official Source

- [Gemma 2 documentation or model card](https://ai.google.dev/gemma/docs/core/model_card_2)
