# DeepSeek-V3.1-Terminus

## The Final Refinement of V3.1

**DeepSeek-V3.1-Terminus**, released in September 2025, is a post-training update to V3.1 rather than a new architecture. It preserves the 671B-parameter MoE backbone, 37B active parameters, and 128K context.

The update targeted problems reported in real use:

- Fewer mixed Chinese-English passages and abnormal characters
- Better code-agent behavior
- Better search-agent behavior
- Updated search tool templates and trajectories

```text
V3.1 architecture + refined post-training → V3.1-Terminus
```

“Terminus” indicates the concluding V3.1 checkpoint. It later served as the comparison base for V3.2-Exp, allowing researchers to isolate the effect of sparse attention.

It retains V3.1's thinking and non-thinking modes. Agent performance still depends on the surrounding tool harness, permissions, parsing, and recovery logic.

## Source

- [Official DeepSeek-V3.1-Terminus model card](https://huggingface.co/deepseek-ai/DeepSeek-V3.1-Terminus)
