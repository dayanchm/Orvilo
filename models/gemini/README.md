# Gemini Model Guide

This directory explains the major generations of Google's Gemini models. Google does not publish parameter counts for these proprietary models, so the comparison focuses on documented capabilities and context limits.

1. [Gemini 1.0](gemini-1.0.md) — native multimodality and Nano/Pro/Ultra tiers
2. [Gemini 1.5](gemini-1.5.md) — Mixture of Experts and million-token context
3. [Gemini 2.0](gemini-2.0.md) — native tool use and live interaction
4. [Gemini 2.5](gemini-2.5.md) — thinking models and computer use
5. [Gemini 3](gemini-3.md) — multimodal reasoning and agentic workflows
6. [Gemini 3.1](gemini-3.1.md) — stronger reasoning, coding, and agents

## Gemini Model Evolution

```mermaid
flowchart TD
    G10["Gemini 1.0<br/>2023 · Native multimodality"]
    NANO["Nano<br/>On-device"]
    PRO10["Pro<br/>General purpose"]
    ULTRA["Ultra<br/>Maximum capability"]

    G15["Gemini 1.5<br/>2024 · MoE + long context"]
    PRO15["1.5 Pro<br/>Complex multimodal tasks"]
    FLASH15["1.5 Flash<br/>Speed and scale"]

    G20["Gemini 2.0<br/>2024–25 · Native tool use"]
    FLASH20["2.0 Flash<br/>Agents + live multimodality"]
    LITE20["2.0 Flash-Lite<br/>Lower cost"]

    G25["Gemini 2.5<br/>2025 · Thinking models"]
    PRO25["2.5 Pro<br/>Advanced reasoning"]
    DEEP25["2.5 Deep Think<br/>Multiple hypotheses"]
    COMPUTER["2.5 Computer Use<br/>UI agents"]

    G30["Gemini 3<br/>2025 · Agentic reasoning"]
    PRO30["3 Pro<br/>Complex tasks"]
    FLASH30["3 Flash<br/>Efficient agents"]
    IMAGE30["3 Pro Image<br/>Generation + editing"]

    G31["Gemini 3.1<br/>2026 · Frontier intelligence with action"]
    PRO31["3.1 Pro<br/>Reasoning + coding"]
    LITE31["3.1 Flash-Lite<br/>High-volume tasks"]
    DEEP31["3.1 Deep Think<br/>Science + engineering"]

    G10 --> G15 --> G20 --> G25 --> G30 --> G31
    G10 --> NANO
    G10 --> PRO10
    G10 --> ULTRA
    G15 --> PRO15
    G15 --> FLASH15
    G20 --> FLASH20
    G20 --> LITE20
    G25 --> PRO25
    G25 --> DEEP25
    G25 --> COMPUTER
    G30 --> PRO30
    G30 --> FLASH30
    G30 --> IMAGE30
    G31 --> PRO31
    G31 --> LITE31
    G31 --> DEEP31

    classDef generation fill:#dbeafe,stroke:#2563eb,color:#172554
    classDef efficient fill:#dcfce7,stroke:#16a34a,color:#052e16
    classDef reasoning fill:#fef3c7,stroke:#d97706,color:#451a03
    classDef multimodal fill:#f3e8ff,stroke:#9333ea,color:#3b0764

    class G10,G15,G20,G25,G30,G31 generation
    class NANO,FLASH15,LITE20,FLASH30,LITE31 efficient
    class ULTRA,PRO15,PRO25,DEEP25,PRO30,PRO31,DEEP31 reasoning
    class PRO10,FLASH20,COMPUTER,IMAGE30 multimodal

    click G10 "gemini-1.0.md" "Read about Gemini 1.0"
    click G15 "gemini-1.5.md" "Read about Gemini 1.5"
    click G20 "gemini-2.0.md" "Read about Gemini 2.0"
    click G25 "gemini-2.5.md" "Read about Gemini 2.5"
    click G30 "gemini-3.md" "Read about Gemini 3"
    click G31 "gemini-3.1.md" "Read about Gemini 3.1"
```

Select a blue generation node to open its detailed English guide.

## Gemini Generation Comparison

| Generation | Released | Main tiers or variants | Documented context | Defining change |
|---|---:|---|---:|---|
| [Gemini 1.0](gemini-1.0.md) | 2023 | Nano, Pro, Ultra | 32K | Native multimodal training |
| [Gemini 1.5](gemini-1.5.md) | 2024 | Pro, Flash, Flash-8B | Up to 1M | MoE and very long context |
| [Gemini 2.0](gemini-2.0.md) | 2024–25 | Flash, Flash-Lite, Pro Experimental | Up to 1M | Native tools and Live API |
| [Gemini 2.5](gemini-2.5.md) | 2025 | Pro, Flash, Flash-Lite, Deep Think, Computer Use | Up to 1M | Thinking and UI agents |
| [Gemini 3](gemini-3.md) | 2025 | Pro, Flash, Pro Image | Up to 1M | Stronger agentic multimodal reasoning |
| [Gemini 3.1](gemini-3.1.md) | 2026 | Pro, Flash-Lite, Deep Think, Image, Audio | Up to 1M | Advanced coding and long-horizon agents |

## Capability Matrix

| Generation | Text | Image input | Audio/video | Long context | Thinking | Tool use | Image output |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Gemini 1.0 | ● | ● | ● | ◐ | ◐ | ◐ | — |
| Gemini 1.5 | ● | ● | ● | ● | ◐ | ● | — |
| Gemini 2.0 | ● | ● | ● | ● | ◐ | ● | ◐ |
| Gemini 2.5 | ● | ● | ● | ● | ● | ● | ● |
| Gemini 3 | ● | ● | ● | ● | ● | ● | ● |
| Gemini 3.1 | ● | ● | ● | ● | ● | ● | ● |

**Legend:** ● primary or strong capability · ◐ partial, variant-dependent, or emerging capability · — not a defining capability

> Generation-level rows summarize a family. Individual Pro, Flash, Lite, Deep Think, Image, and Audio variants can have different inputs, outputs, limits, availability, and pricing.

## Official Sources

- [Google DeepMind Gemini page](https://deepmind.google/models/gemini/)
- [Google DeepMind model cards](https://deepmind.google/models/model-cards/)
