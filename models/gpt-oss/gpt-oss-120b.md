# GPT-OSS 120B

**Released:** August 2025

## Overview

GPT-OSS 120B is OpenAI's higher-capacity open-weight reasoning model for demanding local and private deployments.

## Architecture and Training

The sparse model has about 117B total parameters and 5.1B active parameters per token. It supports 131,072 tokens, adjustable reasoning effort, function calling, structured outputs, and full chain-of-thought access. OpenAI states that it fits on a single 80 GB H100.

## Best Fit

Use it for advanced reasoning, coding, agents, and fine-tuning when the infrastructure budget supports it. The weights use Apache 2.0.

## Limitations

It is text-only and has a June 2024 knowledge cutoff. Tool results and factual answers still need validation.

## Official Source

- [GPT-OSS 120B documentation or model card](https://developers.openai.com/api/docs/models/gpt-oss-120b)
