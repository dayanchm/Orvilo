# Kimi K2

**Released:** July 2025

## Overview

Kimi K2 is an open-weight mixture-of-experts model designed for knowledge, coding, and agentic tool use.

## Architecture and Training

It has roughly one trillion total parameters but activates about 32B per token. Base and instruction variants were released, followed by updated Thinking and long-context checkpoints.

## Best Fit

Use K2 Instruct for general agents and coding, Base for adaptation, and Thinking variants for deliberate reasoning. Sparse activation lowers compute relative to a dense 1T model but not storage.

## Limitations

Serving still requires substantial accelerator memory and expert-parallel infrastructure. Verify the exact checkpoint's context and license.

## Official Source

- [Kimi K2 documentation or model card](https://github.com/MoonshotAI/Kimi-K2)
