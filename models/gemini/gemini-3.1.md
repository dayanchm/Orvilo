# Gemini 3.1

## A More Capable Gemini 3 Generation

**Gemini 3.1**, introduced in February 2026 with Gemini 3.1 Pro, refines the Gemini 3 architecture for complex reasoning, advanced coding, multimodal understanding, and agentic work.

## Gemini 3.1 Pro

Gemini 3.1 Pro accepts:

- Text and PDFs
- Images
- Audio
- Video
- Large code repositories

It supports up to **1M input tokens** and **64K output tokens**. Available tool interfaces include function calling, structured output, search, and code execution.

```text
Multimodal evidence + long context + reasoning + tools
                           ↓
              Complex agentic workflows
```

## Other 3.1 Variants

The broader generation includes variants such as **3.1 Flash-Lite** for efficient high-volume tasks, image models for generation and editing, audio models for live interaction and speech, and **3.1 Deep Think** for more demanding scientific and engineering reasoning.

These variants should not be treated as identical. They share a generation label but differ in latency, modality, output type, tool support, and intended workload.

## What Improved

Google reports stronger performance than Gemini 3 Pro across reasoning, agentic coding, long-context tasks, tool use, and multimodal evaluations. The core product direction is “frontier intelligence with action”: solving a problem across several steps rather than producing only one completion.

## Limitations

Gemini 3.1 can still hallucinate, misinterpret media, make faulty tool calls, or lose important information in very long inputs. Reasoning effort raises cost and latency, and benchmark performance does not guarantee reliability in a specific application.

## Sources

- [Gemini 3.1 Pro model card](https://deepmind.google/models/model-cards/gemini-3-1-pro/)
- [Gemini 3.1 Pro overview](https://deepmind.google/models/gemini/pro/)
