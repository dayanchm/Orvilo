# Mixtral 8x7B

**Mixtral 8x7B**, released in December 2023, is a sparse Mixture-of-Experts model. Each feed-forward layer has eight experts and routes each token to two.

It has about 46.7B total parameters but uses roughly 12.9B parameters per token, with a 32K context. This offers greater capacity than Mistral 7B without dense-model computation at the full parameter count.

Base and instruction variants were released under Apache 2.0.

## Source
- [Mixtral announcement](https://mistral.ai/news/mixtral-of-experts/)
