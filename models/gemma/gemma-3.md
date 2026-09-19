# Gemma 3

**Released:** March 2025

## Overview

Gemma 3 expanded the open family into multilingual, long-context vision-language models.

## Architecture and Training

Sizes include 270M, 1B, 4B, 12B, and 27B. The 4B, 12B, and 27B variants accept images and up to 128K tokens; the smallest variants are text-only with 32K context. The family supports more than 140 languages.

## Best Fit

Use larger variants for document and image understanding, and smaller variants for local or edge text workloads. Function-calling support enables tool-oriented applications.

## Limitations

Image input produces text output; it does not generate images. Context and modality differ by size, so check the selected checkpoint.

## Official Source

- [Gemma 3 documentation or model card](https://ai.google.dev/gemma/docs/core/model_card_3)
