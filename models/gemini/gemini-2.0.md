# Gemini 2.0

## A Model Family Built for the Agentic Era

**Gemini 2.0**, announced in December 2024, expanded Gemini from multimodal understanding toward systems that can interact with tools and real-time environments.

## Main Variants

| Variant | Primary goal |
|---|---|
| Gemini 2.0 Flash | Fast general multimodal and agent workloads |
| Gemini 2.0 Flash-Lite | Cost-sensitive, high-volume tasks |
| Gemini 2.0 Pro Experimental | Experimental higher-capability tier |

Gemini 2.0 Flash and Flash-Lite offered a **1M-token context window**. The Pro model was released experimentally rather than as a general production model.

## Native Tool Use

Gemini 2.0 could choose and call tools such as search, code execution, or application functions.

```text
User request → Plan → Call tool → Read result → Respond or continue
```

This is the foundation of an agent: the model does not only generate an answer but can gather information or take a structured action through an external system.

## Live and Multimodal Interaction

The Multimodal Live API enabled low-latency audio and video streaming. Early 2.0 work also explored native image and audio output, spatial understanding, and conversational image editing.

## Why It Mattered

Gemini 2.0 connected long-context multimodality with action. It shifted the development focus from “understand several modalities” toward “understand, reason, use tools, and continue interacting.”

## Limitations

Tool use creates risks beyond incorrect text. A model can choose the wrong function, pass unsafe arguments, or misread a tool result. Applications need permissions, validation, logging, and human confirmation for consequential actions.

## Sources

- [The next chapter of the Gemini era](https://developers.googleblog.com/the-next-chapter-of-the-gemini-era-for-developers/)
- [Gemini 2.0 model family](https://developers.googleblog.com/en/gemini-2-family-expands/)
