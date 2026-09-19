# Transformer

## What is a Transformer?

A **Transformer** is a neural network architecture introduced in 2017 in the paper **"Attention Is All You Need"** by Ashish Vaswani and colleagues.

Unlike RNNs and LSTMs, Transformers do not need to process a sequence strictly one word at a time.

Instead, they rely heavily on a mechanism called **Self-Attention**.

The basic idea is:

> Every token can look at other relevant tokens in the sequence and determine how much attention to give them.

## Before Transformers

RNNs and LSTMs process sequences step by step.

```text id="1ny5s3"
I → love → programming → in → Go
```

Information moves through the sequence:

```text id="ez8p4g"
word₁ → RNN → state₁
                  ↓
word₂ → RNN → state₂
                  ↓
word₃ → RNN → state₃
```

This sequential structure makes it harder to parallelize computation and can make long-range relationships challenging to learn.

## The Transformer Idea

The Transformer takes a different approach.

Instead of passing information sequentially from one token to the next, tokens can interact through **Self-Attention**.

```text id="3szcbp"
The   animal   didn't   cross   the   street
 ↑       ↑        ↑       ↑      ↑      ↑
 └───────┴────────┴───────┴──────┴──────┘
              Self-Attention
```

Each token can gather information from other tokens in the sequence.

## Self-Attention

Consider:

```text id="mr29zn"
The animal didn't cross the street because it was tired.
```

When processing:

```text id="y47h4m"
it
```

the model may need to determine that `it` is related to:

```text id="my30y7"
animal
```

Self-Attention allows relationships between tokens to be represented directly.

Conceptually:

```text id="66y7ts"
animal ←──────── it
   ↑
strong relationship
```

Different tokens can receive different attention weights.

```text id="jvh1s5"
The      → 0.03
animal   → 0.65
street   → 0.08
it       → 0.12
tired    → 0.12
```

These numbers are only illustrative.

## Query, Key and Value

Transformer Self-Attention introduces three important concepts:

```text id="f71r52"
Query (Q)
Key   (K)
Value (V)
```

Each token representation is transformed into a **Query**, **Key**, and **Value**.

```text id="5jmm54"
Token
  │
  ├──→ Query
  │
  ├──→ Key
  │
  └──→ Value
```

A simple way to think about them is:

```text id="q2a5bv"
Query → What am I looking for?

Key   → What information do I contain?

Value → What information should I provide?
```

The Query of one token is compared with the Keys of other tokens.

```text id="7ef33b"
Query
  ↓
compare with Keys
  ↓
Attention Scores
  ↓
Softmax
  ↓
Attention Weights
  ↓
Weighted Values
  ↓
Output
```

In simplified mathematical form:

```text id="1b4udm"
Attention(Q, K, V)
        =
softmax(QKᵀ / √dₖ)V
```

This is called **Scaled Dot-Product Attention**.

## Multi-Head Attention

Transformers do not use only one attention operation.

They use multiple attention heads.

```text id="6w7mjd"
Input
  │
  ├── Attention Head 1
  ├── Attention Head 2
  ├── Attention Head 3
  └── Attention Head 4
            ↓
         Combine
            ↓
          Output
```

Different heads can learn different kinds of relationships.

For example, some heads may capture syntactic or positional relationships, while others may capture other useful patterns.

## Embeddings

Transformers do not operate directly on words.

Tokens are first converted into numerical vectors.

```text id="7o2ydn"
"Go"
 ↓
Token
 ↓
Embedding
 ↓
[0.21, -0.54, 0.83, ...]
```

So the beginning of the pipeline looks roughly like:

```text id="fqyxzp"
Text
 ↓
Tokenizer
 ↓
Tokens
 ↓
Embeddings
 ↓
Transformer
```

## Positional Information

Because Self-Attention does not inherently process tokens one after another like an RNN, the model needs information about token positions.

For example:

```text id="a7zxjw"
dog bites man

≠

man bites dog
```

The original Transformer added **positional encodings** to token embeddings.

```text id="13dbz7"
Token Embedding
      +
Position Encoding
      ↓
Transformer
```

This gives the model information about where tokens occur in the sequence.

## Transformer Block

A simplified Transformer block looks like:

```text id="u7pk48"
Input
  ↓
Multi-Head Self-Attention
  ↓
Add & Normalize
  ↓
Feed-Forward Network
  ↓
Add & Normalize
  ↓
Output
```

These blocks can be stacked:

```text id="rm9jxg"
Embeddings
    ↓
Transformer Block
    ↓
Transformer Block
    ↓
Transformer Block
    ↓
    ...
    ↓
Final Representations
```

## Encoder and Decoder

The original 2017 Transformer used an **Encoder–Decoder** architecture.

```text id="44bzro"
Input
  ↓
Encoder
  ↓
Representations
  ↓
Decoder
  ↓
Output
```

For example, in machine translation:

```text id="r42fdj"
"I love programming"
        ↓
     Encoder
        ↓
     Decoder
        ↓
"Programlamayı seviyorum"
```

The Transformer replaced the recurrent components used by earlier Seq2Seq systems with attention-based components.

## Why Was the Transformer Important?

The Transformer introduced a powerful way to model relationships across sequences without relying on recurrence.

Compared with RNN/LSTM-based approaches, Transformer architectures allow much more parallel computation during training.

They also became highly effective at modeling relationships across long sequences.

This architecture became the foundation for many modern language models.

## Transformer → Modern Language Models

After the Transformer:

```text id="4jig2i"
2017
Transformer
    ↓
2018
GPT-1
    ↓
2018
BERT
    ↓
2019
GPT-2
    ↓
2020
GPT-3
    ↓
Modern LLMs
```

Different model families use the Transformer in different ways.

For example:

```text id="a1h21j"
BERT
↓
Encoder-based Transformer

GPT
↓
Decoder-based Transformer

Original Transformer
↓
Encoder + Decoder
```

## From Text to Prediction

A simplified modern language-model pipeline looks like:

```text id="52z7zm"
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embeddings
 ↓
Positional Information
 ↓
Transformer Blocks
 ↓
Logits
 ↓
Softmax
 ↓
Next-token probabilities
```

For example:

```text id="9fn3je"
"I love programming in"

          ↓
      Transformer
          ↓

Go      38%
Python  31%
Rust    14%
Java     8%
...
```

The model can select a token and repeat the process:

```text id="xpmw2j"
Input
 ↓
Predict next token
 ↓
Add token to input
 ↓
Predict next token
 ↓
Add token
 ↓
...
```

This autoregressive process is the basic idea behind GPT-style text generation.

## Why Does This Matter?

Many ideas we encountered earlier now come together:

```text id="zbrq4j"
N-gram
↓
Predict language statistically

Neural Language Models
↓
Learn representations

Word Embeddings
↓
Represent words as vectors

Seq2Seq
↓
Transform one sequence into another

Attention
↓
Focus on relevant information

Self-Attention
↓
Tokens interact with other tokens

Transformer
↓
Build the architecture around attention
```

The Transformer became one of the key foundations of modern Large Language Models.

## What's Next?

The Transformer gives us the architecture.

The next question is:

> How do we use a Transformer to train a model that can generate language?

This leads to **GPT — Generative Pre-trained Transformer**.