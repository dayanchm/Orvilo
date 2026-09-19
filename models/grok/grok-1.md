# Grok 1

**Released:** November 2023; weights released March 2024

## Overview

Grok 1 was xAI's first public model and the foundation of the Grok assistant, which was designed to combine general conversation with timely information from X.

## Architecture and Training

The released base checkpoint is a 314B-parameter mixture-of-experts model that activates a subset of experts for each token. xAI published the weights under Apache 2.0 without the later product's search or alignment systems.

## Best Fit

Use the open base model for architecture research and large-scale fine-tuning; use the hosted product when live tools and assistant behavior are required.

## Limitations

The base checkpoint is expensive to host, has an 8K context, and is not the same as the continuously updated Grok service.

## Official Source

- [Grok 1 documentation or model card](https://github.com/xai-org/grok-1)
