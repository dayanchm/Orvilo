# Gemini 3

## Multimodal Reasoning with Stronger Agent Capabilities

**Gemini 3**, introduced in November 2025, is a family of natively multimodal reasoning models built for complex problem solving, coding, creative work, and agents.

## Main Variants

- **Gemini 3 Pro** for the most demanding general tasks in the original 3.0 release
- **Gemini 3 Flash** for faster, more efficient reasoning and agent workloads
- **Gemini 3 Pro Image** for image generation and conversational editing

## From Tool Use to Agentic Work

Gemini 2.0 introduced native tool use. Gemini 3 emphasized longer multi-step workflows:

```text
Goal → Plan → Use tools → Inspect results → Revise plan → Finish
```

This supports repository-level coding, research, information synthesis, and tasks in which the model must recover when an intermediate step fails.

## Native Multimodal Reasoning

The family works across text, images, audio, video, PDFs, and code. The important distinction is not merely accepting these formats, but combining evidence across them while reasoning.

## Gemini 3 Pro Image

The image variant—also known as **Nano Banana Pro**—uses Gemini's reasoning and world knowledge for text-to-image generation and multi-turn image editing. It belongs to the Gemini 3 family but serves a different output modality than the text-oriented Pro model.

## Why It Mattered

Gemini 3 strengthened the connection between multimodal reasoning and action. Coding, tool use, long-context synthesis, and visual understanding became parts of the same agent-oriented system.

## Limitations

Agents may compound errors across steps. Generated images may contain inaccuracies, and text models can still hallucinate or overlook evidence. Tool access must be sandboxed and audited.

## Sources

- [Official Gemini model page](https://deepmind.google/models/gemini/)
- [Google DeepMind model cards](https://deepmind.google/models/model-cards/)
