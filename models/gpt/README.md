# GPT Model Guide

This directory explains the evolution of OpenAI's GPT family. Parameter counts are shown only when OpenAI published them.

## GPT Evolution

```mermaid
flowchart TD
    G1["GPT-1 · 2018<br/>Pretrain + fine-tune"] --> G2["GPT-2 · 2019<br/>Zero-shot emergence"]
    G2 --> G3["GPT-3 · 2020<br/>In-context learning"]
    G3 --> I["InstructGPT · 2022<br/>RLHF"]
    I --> G35["GPT-3.5 · 2022<br/>Chat optimization"]
    G35 --> G4["GPT-4 · 2023<br/>Multimodal reasoning"]
    G4 --> T["GPT-4 Turbo · 2023<br/>128K context"]
    T --> O["GPT-4o · 2024<br/>Omni multimodality"]
    O --> OM["GPT-4o Mini<br/>Efficient model"]
    O --> G41["GPT-4.1 · 2025<br/>1M non-reasoning"]
    G4 --> G45["GPT-4.5 · 2025<br/>Scaled pretraining"]
    G41 --> G5["GPT-5 · 2025<br/>Configurable reasoning"]
    G45 --> G5
    G5 --> G55["GPT-5.5<br/>Professional work"]
    G55 --> G56["GPT-5.6<br/>Sol · Terra · Luna"]
    G56 --> G6["GPT-6 Astra · 2026<br/>End-to-end agents"]

    classDef early fill:#dbeafe,stroke:#2563eb,color:#172554
    classDef alignment fill:#dcfce7,stroke:#16a34a,color:#052e16
    classDef multimodal fill:#f3e8ff,stroke:#9333ea,color:#3b0764
    classDef reasoning fill:#fef3c7,stroke:#d97706,color:#451a03
    classDef latest fill:#ffe4e6,stroke:#e11d48,color:#4c0519
    class G1,G2,G3 early
    class I,G35 alignment
    class G4,T,O,OM,G41,G45 multimodal
    class G5,G55,G56 reasoning
    class G6 latest

    click G1 "gpt-1.md" "Read GPT-1"
    click G2 "gpt-2.md" "Read GPT-2"
    click G3 "gpt-3.md" "Read GPT-3"
    click I "instructgpt.md" "Read InstructGPT"
    click G35 "gpt-3.5.md" "Read GPT-3.5"
    click G4 "gpt-4.md" "Read GPT-4"
    click T "gpt-4-turbo.md" "Read GPT-4 Turbo"
    click O "gpt-4o.md" "Read GPT-4o"
    click OM "gpt-4o-mini.md" "Read GPT-4o Mini"
    click G41 "gpt-4.1.md" "Read GPT-4.1"
    click G45 "gpt-4.5.md" "Read GPT-4.5"
    click G5 "gpt-5.md" "Read GPT-5"
    click G55 "gpt-5.5.md" "Read GPT-5.5"
    click G56 "gpt-5.6.md" "Read GPT-5.6"
    click G6 "gpt-6-astra.md" "Read GPT-6 Astra"
```

## Model Comparison

| Model | Released | Published size | Context | Defining change |
|---|---:|---:|---:|---|
| [GPT-1](gpt-1.md) | 2018 | 117M | 512 | Generative pretraining and fine-tuning |
| [GPT-2](gpt-2.md) | 2019 | 1.5B | 1K | Zero-shot task behavior |
| [GPT-3](gpt-3.md) | 2020 | 175B | 2K | In-context few-shot learning |
| [InstructGPT](instructgpt.md) | 2022 | 1.3B–175B experiments | 2K | RLHF and instruction following |
| [GPT-3.5](gpt-3.5.md) | 2022 | Not disclosed | Up to 16K | Accessible conversational AI |
| [GPT-4](gpt-4.md) | 2023 | Not disclosed | 8K / 32K | Stronger reasoning and vision |
| [GPT-4 Turbo](gpt-4-turbo.md) | 2023 | Not disclosed | 128K | Longer context and lower cost |
| [GPT-4o](gpt-4o.md) | 2024 | Not disclosed | 128K | Native omni multimodality |
| [GPT-4o Mini](gpt-4o-mini.md) | 2024 | Not disclosed | 128K | Affordable multimodal model |
| [GPT-4.1](gpt-4.1.md) | 2025 | Not disclosed | 1M | Coding and non-reasoning agents |
| [GPT-4.5](gpt-4.5.md) | 2025 | Not disclosed | 128K | Scaled unsupervised learning |
| [GPT-5](gpt-5.md) | 2025 | Not disclosed | 400K | Mainstream configurable reasoning |
| [GPT-5.5](gpt-5.5.md) | 2026 | Not disclosed | 400K | Coding and professional work |
| [GPT-5.6](gpt-5.6.md) | 2026 | Not disclosed | 1.05M | Sol, Terra, and Luna tiers |
| [GPT-6 Astra](gpt-6-astra.md) | 2026 | Not disclosed | 1.05M | Long-running end-to-end agents |

## Capability Matrix

| Generation | Chat | Vision | Reasoning control | Tools | Long context | Agents |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| GPT-1–3 | ◐ | — | — | — | — | — |
| InstructGPT / GPT-3.5 | ● | — | — | ◐ | — | — |
| GPT-4 / Turbo | ● | ● | — | ● | ◐ | ◐ |
| GPT-4o family | ● | ● | — | ● | ◐ | ● |
| GPT-4.1 / 4.5 | ● | ● | — | ● | ● | ● |
| GPT-5 family | ● | ● | ● | ● | ● | ● |
| GPT-6 Astra | ● | ● | ● | ● | ● | ● |

**Legend:** ● primary or strong capability · ◐ partial or emerging capability · — not a defining capability

For the combined long-form explanation of GPT-1 through GPT-3, see [GPT fundamentals](gpt.md).

## Official Sources

- [OpenAI model catalog](https://developers.openai.com/api/docs/models/all)
- [OpenAI model guidance](https://developers.openai.com/api/docs/guides/latest-model)
