# Tokenization

Tokenization converts raw input into discrete token IDs that a model can process. The tokenizer defines the model's vocabulary and therefore affects sequence length, multilingual efficiency, code handling, and generation behavior.

## Encoding and Decoding

~~~mermaid
flowchart LR
    T["unbelievable"] --> N["Normalize"]
    N --> S["Split into tokens"]
    S --> I["Token IDs"]
    I --> E["Embedding vectors"]
    O["Generated IDs"] --> D["Decode"]
    D --> X["Output text"]
~~~

A subword tokenizer might represent a rare word as “un”, “believ”, and “able” while keeping a frequent word as one token.

## Common Approaches

| Method | Idea | Tradeoff |
|---|---|---|
| Word-level | One vocabulary item per word | Huge vocabulary and unknown words |
| Character-level | One token per character | Long sequences |
| Byte-level | Operate over bytes | Universal coverage, less readable tokens |
| BPE | Repeatedly merge common pairs | Efficient and widely used |
| WordPiece | Choose merges using a language-model objective | Strong subword vocabulary |
| Unigram | Select likely pieces from a candidate vocabulary | Flexible probabilistic segmentation |
| SentencePiece | Train directly on raw text | Language-independent preprocessing |

Modern tokenizers often combine subword algorithms with byte fallback.

## Vocabulary Design

A larger vocabulary can shorten sequences but increases embedding and output layers. A smaller vocabulary shares pieces across words but requires more positions.

Evaluate token fertility: the average number of tokens per word or character. Poor fertility in a language makes its text more expensive and reduces how much fits in a context window.

## Special Tokens

Models may reserve tokens for sequence boundaries, padding, unknown bytes, chat roles, tool calls, images, audio, or fill-in-the-middle code.

Special-token meaning is part of the model contract. Adding or reassigning tokens after pretraining requires careful embedding initialization and training.

## Chat Templates

Instruction models convert messages into a token sequence using a chat template:

~~~text
<system>You are helpful.</system>
<user>Summarize this.</user>
<assistant>
~~~

The exact representation differs by model. Using the wrong template can reduce quality or break tool calling.

## Training a Tokenizer

1. choose representative multilingual and domain data;
2. decide normalization and byte fallback;
3. set vocabulary size and special tokens;
4. train the segmentation model;
5. evaluate fertility, reversibility, and edge cases;
6. freeze and version the tokenizer before model training.

Test whitespace, Unicode normalization, emoji, combining characters, source code, numbers, URLs, and invalid byte sequences.

## Security and Reliability

Visually identical Unicode can tokenize differently. Token boundaries can also affect filters and prompt-injection defenses. Perform security checks on normalized and decoded forms, not only visible strings.

Never estimate cost or context from character count alone.

## Related Guides

- [Datasets](datasets.md)
- [Embeddings](embeddings.md)
- [Pretraining](pretraining.md)
