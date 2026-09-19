# GPT-OSS 20B

**Released:** August 2025

## Overview

GPT-OSS 20B is OpenAI's smaller open-weight reasoning model, designed for local or specialized use with relatively modest memory.

## Architecture and Training

It has about 21B total parameters and activates about 3.6B per token through a mixture-of-experts architecture. It supports a 131,072-token context, configurable reasoning effort, tool calling, structured output, and visible chain-of-thought.

## Best Fit

The model can run in roughly 16 GB of memory with suitable quantization/runtime choices and is useful for local agents, coding, and task-specific fine-tuning.

## Limitations

It is text-only, can hallucinate, and requires an application-level safety layer. Visible reasoning should not automatically be shown to end users.

## Official Source

- [GPT-OSS 20B documentation or model card](https://developers.openai.com/api/docs/models/gpt-oss-20b)
