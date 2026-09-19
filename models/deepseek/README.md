# DeepSeek Model Guide

This directory explains the development of DeepSeek's main language and code models. Read the documents roughly in this order:

1. [DeepSeek LLM](deepseek-llm.md) — first general English-Chinese models
2. [DeepSeek Coder](deepseek-coder.md) — first code-focused family
3. [DeepSeek-V2](deepseek-v2.md) — DeepSeekMoE and Multi-head Latent Attention
4. [DeepSeek-Coder-V2](deepseek-coder-v2.md) — V2 architecture specialized for code
5. [DeepSeek-V2.5](deepseek-v2.5.md) — combined chat and coding model
6. [DeepSeek-V3](deepseek-v3.md) — larger, efficiently trained MoE model
7. [DeepSeek-R1](deepseek-r1.md) — reinforcement-learning-based reasoning
8. [DeepSeek-V3.1](deepseek-v3.1.md) — hybrid thinking and tool use
9. [DeepSeek-V3.1-Terminus](deepseek-v3.1-terminus.md) — refined V3.1 release
10. [DeepSeek-V3.2-Exp](deepseek-v3.2-exp.md) — experimental sparse attention
11. [DeepSeek-V3.2](deepseek-v3.2.md) — reasoning and agentic model
12. [DeepSeek-V3.2-Speciale](deepseek-v3.2-speciale.md) — high-compute reasoning variant
13. [DeepSeek-V4](deepseek-v4.md) — million-token V4 family
14. [DeepSeek-V4-Flash](deepseek-v4-flash.md) — efficient V4 variant
15. [DeepSeek-V4-Pro](deepseek-v4-pro.md) — high-capacity V4 variant
16. [DeepSeek-V4.1-Flash](deepseek-v4.1-flash.md) — multimodal asymmetric architecture

Model names with dates or labels such as `Exp`, `Terminus`, and `Speciale` are specific revisions or variants; they are not entirely separate model generations.



## DeepSeek Model Evolution

```mermaid
flowchart TD
    LLM["DeepSeek LLM<br/>2023 · Dense foundation models"]
    CODER["DeepSeek Coder<br/>2023 · Code specialization"]

    V2["DeepSeek-V2<br/>2024 · MoE + MLA"]
    CODERV2["DeepSeek-Coder-V2<br/>2024 · 128K code model"]
    V25["DeepSeek-V2.5<br/>2024 · General + coding"]

    V3["DeepSeek-V3<br/>2024 · 671B MoE"]
    R1["DeepSeek-R1<br/>2025 · RL reasoning"]
    V31["DeepSeek-V3.1<br/>2025 · Hybrid thinking"]
    TERMINUS["V3.1-Terminus<br/>2025 · Agent refinement"]
    V32EXP["V3.2-Exp<br/>2025 · Sparse-attention experiment"]
    V32["DeepSeek-V3.2<br/>2025 · Reasoning + agents"]
    SPECIALE["V3.2-Speciale<br/>High-compute reasoning"]

    V4["DeepSeek-V4<br/>2026 · 1M context"]
    FLASH["V4-Flash<br/>Efficient variant"]
    PRO["V4-Pro<br/>High-capacity variant"]
    V41["V4.1-Flash<br/>2026 · Multimodal asymmetric model"]

    LLM --> V2
    CODER --> CODERV2
    V2 --> CODERV2
    V2 --> V25
    CODERV2 --> V25
    V25 --> V3
    V3 --> R1
    V3 --> V31
    R1 -. reasoning behavior .-> V31
    V31 --> TERMINUS
    TERMINUS --> V32EXP
    V32EXP --> V32
    V32 --> SPECIALE
    V32 --> V4
    V4 --> FLASH
    V4 --> PRO
    FLASH --> V41

    classDef foundation fill:#dbeafe,stroke:#2563eb,color:#172554
    classDef code fill:#dcfce7,stroke:#16a34a,color:#052e16
    classDef reasoning fill:#fef3c7,stroke:#d97706,color:#451a03
    classDef agent fill:#f3e8ff,stroke:#9333ea,color:#3b0764
    classDef latest fill:#ffe4e6,stroke:#e11d48,color:#4c0519

    class LLM,V2,V25,V3 foundation
    class CODER,CODERV2 code
    class R1,SPECIALE reasoning
    class V31,TERMINUS,V32EXP,V32 agent
    class V4,FLASH,PRO,V41 latest

    click LLM "deepseek-llm.md" "Read about DeepSeek LLM"
    click CODER "deepseek-coder.md" "Read about DeepSeek Coder"
    click V2 "deepseek-v2.md" "Read about DeepSeek-V2"
    click CODERV2 "deepseek-coder-v2.md" "Read about DeepSeek-Coder-V2"
    click V25 "deepseek-v2.5.md" "Read about DeepSeek-V2.5"
    click V3 "deepseek-v3.md" "Read about DeepSeek-V3"
    click R1 "deepseek-r1.md" "Read about DeepSeek-R1"
    click V31 "deepseek-v3.1.md" "Read about DeepSeek-V3.1"
    click TERMINUS "deepseek-v3.1-terminus.md" "Read about V3.1-Terminus"
    click V32EXP "deepseek-v3.2-exp.md" "Read about V3.2-Exp"
    click V32 "deepseek-v3.2.md" "Read about DeepSeek-V3.2"
    click SPECIALE "deepseek-v3.2-speciale.md" "Read about V3.2-Speciale"
    click V4 "deepseek-v4.md" "Read about DeepSeek-V4"
    click FLASH "deepseek-v4-flash.md" "Read about V4-Flash"
    click PRO "deepseek-v4-pro.md" "Read about V4-Pro"
    click V41 "deepseek-v4.1-flash.md" "Read about V4.1-Flash"
```

The diagram is interactive: select a model to open its detailed English guide. Colors distinguish foundation models, code models, reasoning models, agent-oriented releases, and the V4 family.

## DeepSeek Model Comparison

| Model | Total parameters | Active parameters | Context | Primary focus | Defining feature |
|---|---:|---:|---:|---|---|
| [DeepSeek LLM](deepseek-llm.md) | 7B / 67B | Dense | 4K | General language | Dense Transformer |
| [DeepSeek Coder](deepseek-coder.md) | 1B–33B | Dense | 16K | Code | Project-level code and FIM |
| [DeepSeek-V2](deepseek-v2.md) | 236B | 21B | 128K | General language | DeepSeekMoE and MLA |
| [DeepSeek-Coder-V2](deepseek-coder-v2.md) | 16B / 236B | 2.4B / 21B | 128K | Code | MoE, MLA, and 338 languages |
| [DeepSeek-V2.5](deepseek-v2.5.md) | 236B | 21B | 128K | General + code | Unified Chat and Coder model |
| [DeepSeek-V3](deepseek-v3.md) | 671B | 37B | 128K | General language | FP8 and multi-token prediction |
| [DeepSeek-R1](deepseek-r1.md) | 671B | 37B | 128K | Deep reasoning | Reinforcement learning |
| [DeepSeek-V3.1](deepseek-v3.1.md) | 671B | 37B | 128K | Hybrid reasoning | Thinking modes and tools |
| [V3.1-Terminus](deepseek-v3.1-terminus.md) | 671B | 37B | 128K | Agents | Refined agent behavior |
| [V3.2-Exp](deepseek-v3.2-exp.md) | 671B | 37B | 128K | Long-context efficiency | Sparse-attention experiment |
| [DeepSeek-V3.2](deepseek-v3.2.md) | 671B | 37B | 128K | Reasoning + agents | DSA and reasoning with tools |
| [V3.2-Speciale](deepseek-v3.2-speciale.md) | 671B | 37B | 128K | Maximum reasoning | High compute; no tool calling |
| [DeepSeek-V4](deepseek-v4.md) | 284B–1.6T | 13B–49B | 1M | Long-running agents | Long-context MoE family |
| [V4-Flash](deepseek-v4-flash.md) | 284B | 13B | 1M | Efficient agents | Smaller V4 variant |
| [V4-Pro](deepseek-v4-pro.md) | 1.6T | 49B | 1M | High-capacity agents | Largest V4 variant |
| [V4.1-Flash](deepseek-v4.1-flash.md) | 552B | 8B input / 16B output | — | Multimodal agents | Asymmetric encoder-decoder |

### Capability Matrix

| Model family | Chat | Code | Reasoning | Tools | Long context | Vision |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| DeepSeek LLM | ● | ◐ | — | — | — | — |
| DeepSeek Coder | ◐ | ● | — | — | ◐ | — |
| DeepSeek-V2 | ● | ● | ◐ | ◐ | ● | — |
| DeepSeek-Coder-V2 | ● | ● | ◐ | ◐ | ● | — |
| DeepSeek-V2.5 | ● | ● | ◐ | ● | ● | — |
| DeepSeek-V3 | ● | ● | ◐ | ● | ● | — |
| DeepSeek-R1 | ◐ | ● | ● | ◐ | ● | — |
| DeepSeek-V3.1 | ● | ● | ● | ● | ● | — |
| DeepSeek-V3.2 | ● | ● | ● | ● | ● | — |
| V3.2-Speciale | ◐ | ● | ● | — | ● | — |
| DeepSeek-V4-Flash | ● | ● | ● | ● | ● | — |
| DeepSeek-V4-Pro | ● | ● | ● | ● | ● | — |
| DeepSeek-V4.1-Flash | ● | ● | ● | ● | ● | ● |

**Legend:** ● primary or strong capability · ◐ secondary capability · — not a defining capability

> Parameter count alone does not measure quality. MoE models activate only part of their total parameters for each token, and a larger context window does not guarantee perfect recall.
