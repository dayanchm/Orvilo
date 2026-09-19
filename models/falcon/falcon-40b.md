# Falcon 40B

**Released:** May 2023

## Overview

Falcon 40B is a decoder-only open-weight language model trained primarily on TII's filtered RefinedWeb corpus.

## Architecture and Training

It uses multi-query attention to reduce key/value-cache cost and was released as base and instruction-tuned checkpoints. The original context window is 2,048 tokens.

## Best Fit

It is historically important as a capable openly released 2023 model and remains useful for reproducibility and fine-tuning research.

## Limitations

A 40B model requires substantial memory, and newer families generally provide longer context and stronger instruction following.

## Official Source

- [Falcon 40B documentation or model card](https://huggingface.co/tiiuae/falcon-40b)
