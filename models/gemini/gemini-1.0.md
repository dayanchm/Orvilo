# Gemini 1.0

## Google's First Gemini Generation

**Gemini 1.0**, announced in December 2023, introduced a family of natively multimodal, decoder-only Transformer models. Unlike a text model that receives visual information only through a separate adapter, Gemini was trained jointly on text, images, audio, and video.

## Model Sizes

| Variant | Intended role |
|---|---|
| Gemini Nano | Efficient on-device tasks |
| Gemini Pro | General-purpose deployment at scale |
| Gemini Ultra | The most capable model for complex tasks |

Google did not publicly disclose their parameter counts. The names describe product tiers, not precise model sizes.

## Native Multimodality

```text
Text ──┐
Image ─┼─→ Shared multimodal model → Text response
Audio ─┤
Video ─┘
```

Gemini 1.0 learned representations across modalities during training. This enabled tasks such as explaining a diagram, comparing images, transcribing speech, reasoning over video frames, and combining visual evidence with a written question.

The models supported a context length of up to **32K tokens** and used techniques including multi-query attention for more efficient inference.

## Training and Adaptation

After multimodal pretraining, Google created post-trained variants for Gemini applications and developer APIs. Post-training improved instruction following, conversational behavior, safety, and usefulness.

## Why It Mattered

Gemini 1.0 established the main ideas that continued across the family: native multimodality, several performance tiers, TPU-based training, and integration with tools and Google products.

## Limitations

The model could hallucinate, misunderstand visual details, make reasoning errors, and reproduce biases from training data. A multimodal input does not guarantee that every part of an image, recording, or video is interpreted correctly.

## Source

- [Gemini 1.0 technical report](https://deepmind.google/gemini/gemini_1_report.pdf)
