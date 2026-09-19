# Anthropic Claude Model Guide

Claude is Anthropic's family of conversational and agentic AI models. The family evolved from long-context text assistants into multimodal, hybrid-reasoning systems for coding, computer use, tools, research, and long-running agents.

## Evolution

~~~mermaid
flowchart LR
    C1["Claude 1<br/>Constitutional AI"] --> C2["Claude 2 / 2.1<br/>100K–200K context"]
    C2 --> C3["Claude 3<br/>Haiku · Sonnet · Opus"]
    C3 --> C35["Claude 3.5<br/>Coding + computer use"]
    C35 --> C37["Claude 3.7<br/>Hybrid reasoning"]
    C37 --> C4["Claude 4<br/>Agentic coding"]
    C4 --> C45["Claude 4.5–4.8<br/>Long-running agents"]
    C45 --> C5["Claude 5<br/>Sonnet · Opus"]
    C5 --> F5["Fable 5 / 5.1<br/>Safeguarded frontier"]
    C5 --> M5["Mythos 5 / 5.1<br/>Trusted access"]

    click C1 "claude-1.md"
    click C2 "claude-2.md"
    click C3 "claude-3-sonnet.md"
    click C35 "claude-3.5-sonnet.md"
    click C37 "claude-3.7-sonnet.md"
    click C4 "claude-sonnet-4.md"
    click C45 "claude-sonnet-4.5.md"
    click C5 "claude-sonnet-5.md"
    click F5 "claude-fable-5.1.md"
    click M5 "claude-mythos-5.1.md"
~~~

## What the Tier Names Mean

| Tier | Design goal | Typical use |
|---|---|---|
| **Haiku** | Highest speed and lowest cost | Classification, extraction, chat, worker agents |
| **Sonnet** | Balanced frontier capability | Coding, tools, agents, general professional work |
| **Opus** | Greater depth and reliability | Complex reasoning, research, large codebases |
| **Fable** | Safeguarded capability above Opus | Hardest generally available research and engineering |
| **Mythos** | Restricted dual-use frontier | Vetted cybersecurity and life-sciences research |

Tier names describe product positioning, not a permanent ranking. A newer Haiku can outperform an older Sonnet on some tasks.

## Historical Generations

| Model | Released | Context | Inputs | Defining change |
|---|---:|---:|---|---|
| [Claude 1](claude-1.md) | 2023-03 | Expanded during generation | Text | First Claude assistant |
| [Claude 2](claude-2.md) | 2023-07 | 100K | Text | Long documents and stronger reasoning |
| [Claude 2.1](claude-2.1.md) | 2023-11 | 200K | Text | Greater honesty and enterprise controls |
| [Claude 3 Haiku](claude-3-haiku.md) | 2024-03 | 200K | Text + image | Fast multimodal tier |
| [Claude 3 Sonnet](claude-3-sonnet.md) | 2024-03 | 200K | Text + image | Balanced multimodal tier |
| [Claude 3 Opus](claude-3-opus.md) | 2024-03 | 200K | Text + image | Premium intelligence tier |
| [Claude 3.5 Sonnet](claude-3.5-sonnet.md) | 2024-06 | 200K | Text + image | Coding and computer use |
| [Claude 3.5 Haiku](claude-3.5-haiku.md) | 2024-10 | 200K | Text | Efficient coding and tools |
| [Claude 3.7 Sonnet](claude-3.7-sonnet.md) | 2025-02 | 200K | Text + image | First hybrid reasoning model |

These dated models are useful for understanding the family's evolution, but most are retired from the Claude API. Consult Anthropic's lifecycle page before maintaining an older integration.

## Claude 4 Series

| Model | Released | Context | Main focus |
|---|---:|---:|---|
| [Claude Sonnet 4](claude-sonnet-4.md) | 2025-05 | 200K | Balanced agentic coding |
| [Claude Opus 4](claude-opus-4.md) | 2025-05 | 200K | Advanced agents and coding |
| [Claude Opus 4.1](claude-opus-4.1.md) | 2025-08 | 200K | More precise agentic work |
| [Claude Sonnet 4.5](claude-sonnet-4.5.md) | 2025-09 | 200K | Coding, computer use, agents |
| [Claude Haiku 4.5](claude-haiku-4.5.md) | 2025-10 | 200K | Fast near-frontier work |
| [Claude Opus 4.5](claude-opus-4.5.md) | 2025-11 | 200K | Complex coding and professional work |
| [Claude Opus 4.6](claude-opus-4.6.md) | 2026-02 | Up to 1M beta | Long context and deep agents |
| [Claude Sonnet 4.6](claude-sonnet-4.6.md) | 2026-02 | Up to 1M beta | Efficient long-context agents |
| [Claude Opus 4.7](claude-opus-4.7.md) | 2026-04 | Up to 1M | Coding, vision, multi-step tasks |
| [Claude Opus 4.8](claude-opus-4.8.md) | 2026-05 | 1M | Long-running agents and fallback role |

Context availability can depend on platform, feature flags, and beta status.

## Claude 5 and Frontier Tiers

| Model | Released | Access | Positioning |
|---|---:|---|---|
| [Claude Sonnet 5](claude-sonnet-5.md) | 2026-06 | General | Efficient frontier coding and agents |
| [Claude Opus 5](claude-opus-5.md) | 2026-07 | General | High-capability general model |
| [Claude Fable 5](claude-fable-5.md) | 2026-06 | General with safeguards | Mythos-class base with defense in depth |
| [Claude Mythos 5](claude-mythos-5.md) | 2026-06 | Vetted organizations | Reduced safeguards for qualified research |
| [Claude Fable 5.1](claude-fable-5.1.md) | 2026-09 | General with safeguards | Strongest safeguarded coding and knowledge work |
| [Claude Mythos 5.1](claude-mythos-5.1.md) | 2026-09 | Trusted access | Advanced cyber and biology research |

Fable and Mythos are distinguished partly by access and safeguards. They should not be treated as ordinary replacements for Haiku, Sonnet, or Opus.

## Capability Matrix

| Generation | Vision | Long context | Tool use | Extended thinking | Computer use | General API |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| Claude 1–2.1 | — | ● | ◐ | — | — | Retired |
| Claude 3 | ● | ● | ● | — | — | Retired |
| Claude 3.5 | Variant | ● | ● | — | ● | Retired |
| Claude 3.7 | ● | ● | ● | ● | ● | Retired |
| Claude 4.x | ● | ● | ● | ● | ● | Model-dependent |
| Sonnet / Opus 5 | ● | ● | ● | ● | ● | ● |
| Fable 5.x | ● | ● | ● | ● | ● | Safeguarded |
| Mythos 5.x | ● | ● | ● | ● | ● | Restricted |

**Legend:** ● supported or defining · ◐ early/limited · — not defining

## How to Choose

- Start with **Haiku** when latency and cost dominate.
- Start with **Sonnet** for most coding, tool-use, and production agent workloads.
- Choose **Opus** for difficult tasks where additional depth justifies higher cost.
- Choose **Fable** only when its higher capability and stricter safeguards fit the workload.
- **Mythos** requires vetted access and specialized governance.
- Pin a dated API model ID for reproducibility and monitor Anthropic's deprecation notices.
- Evaluate quality, latency, token usage, tool behavior, and safety on your own tasks.

## Safety Notes

Vision, browser control, code execution, and tools expose models to untrusted content. Use least-privilege credentials, isolate execution, validate tool arguments, log actions, and require approval before irreversible or external side effects.

Long context does not equal perfect memory. Retrieval quality can fall as documents become larger, and stale or malicious content can influence an agent.

## Official Sources

- [Claude model overview](https://docs.anthropic.com/en/docs/about-claude/models/overview)
- [Model lifecycle and deprecations](https://docs.anthropic.com/en/docs/about-claude/model-deprecations)
- [Anthropic newsroom](https://www.anthropic.com/news)
- [Claude Opus](https://www.anthropic.com/claude/opus)
- [Claude Fable](https://www.anthropic.com/claude/fable)
- [Claude Mythos](https://www.anthropic.com/claude/mythos)
