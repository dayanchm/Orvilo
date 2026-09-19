# CodeGemma

**Released:** April 2024

## Overview

CodeGemma adapts Gemma for programming tasks and supports both generation and code completion.

## Architecture and Training

The release includes 2B and 7B pretrained code models plus a 7B instruction-tuned model. Training used primarily code, along with mathematics and natural-language data. Fill-in-the-middle lets the model complete code between a prefix and suffix.

## Best Fit

Choose the 2B variant for low-latency completion and the 7B instruction model for conversational coding help. Supported languages and quality vary, so compile, test, and review generated code.

## Limitations

It inherits Gemma's context and license constraints and should not be treated as a security reviewer.

## Official Source

- [CodeGemma documentation or model card](https://ai.google.dev/gemma/docs/codegemma)
