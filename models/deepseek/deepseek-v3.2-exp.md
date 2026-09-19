# DeepSeek-V3.2-Exp

## An Experiment in Sparse Long-Context Attention

**DeepSeek-V3.2-Exp** is an experimental 2025 release built on V3.1-Terminus. Its purpose was to test **DeepSeek Sparse Attention (DSA)** while keeping other training conditions closely aligned with the earlier model.

DSA adds a lightweight indexer that ranks earlier tokens and selects a subset for full attention:

```text
All earlier tokens → Indexer → Most relevant tokens → Main attention
```

Dense attention grows quadratically with sequence length. Selecting a smaller subset reduces training and inference cost for long contexts. The design is fine-grained: selection happens at token level rather than using only fixed local blocks.

V3.2-Exp is best understood as an architectural validation checkpoint, not the finished V3.2 reasoning model. Its open kernels and matched comparison with V3.1-Terminus helped show whether efficiency gains came from DSA rather than unrelated training changes.

Sparse selection introduces a risk: the indexer may omit information that later turns out to matter. Long-context efficiency therefore does not imply perfect retrieval.

## Source

- [Official DeepSeek-V3.2-Exp model card](https://huggingface.co/deepseek-ai/DeepSeek-V3.2-Exp)
