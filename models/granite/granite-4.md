# Granite 4

**Released:** October 2025

## Overview

Granite 4 introduces hybrid Mamba-2/Transformer models to reduce memory use in long-context and multi-session workloads.

## Architecture and Training

The lineup ranges from 350M and 1B edge models to 3B dense models and MoE variants: H-Tiny is 7B total/1B active, while H-Small is 32B total/9B active. IBM releases them under Apache 2.0.

## Best Fit

Use hybrid variants for efficient RAG and agents, or conventional Transformer variants where runtime support for Mamba-2 is immature.

## Limitations

Performance depends on optimized runtime support. Follow the exact chat template and distinguish total from active parameters.

## Official Source

- [Granite 4 documentation or model card](https://www.ibm.com/granite/docs/models/granite4-0)
