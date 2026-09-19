# DeepSeek-V4-Flash

## The Efficient V4 Variant

**DeepSeek-V4-Flash**, released in 2026, is the smaller and faster member of the original V4 family.

| Property | Value |
|---|---:|
| Total parameters | 284B |
| Active per token | 13B |
| Context window | 1M tokens |

Flash uses an MoE architecture, so its total capacity is much larger than the computation used for one token. It targets high-throughput chat, coding, agent, and long-document workloads.

The model supports non-thinking, Think High, and Think Max modes. Its one-million-token window can hold long agent traces, but does not guarantee perfect recall or reasoning across the entire prompt.

Flash trades some capacity for lower serving cost compared with V4-Pro. In September 2026 it was succeeded in the API by V4.1-Flash; old API aliases may therefore route to a newer model rather than the original checkpoint.

## Sources

- [Official DeepSeek-V4 model overview](https://www.deepseek.com/en/transparency/)
- [DeepSeek API change log](https://api-docs.deepseek.com/updates/)
