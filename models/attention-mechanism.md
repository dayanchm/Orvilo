# Attention

## What is Attention?

**Attention is not a model by itself. It is a mechanism.**

Attention allows a neural network to focus on different parts of the input depending on what information is important at a particular moment.

The basic idea is:

> Instead of compressing all input information into a single fixed representation, let the model look back at the input and decide which parts are most relevant.

## The Problem Before Attention

Early Seq2Seq models commonly used an **Encoder–Decoder** architecture.

```text id="bzvv0x"
Input Sequence
      ↓
    Encoder
      ↓
One Context Vector
      ↓
    Decoder
      ↓
Output Sequence
```

The encoder attempted to compress the entire input sequence into a single fixed-size context vector.

For example:

```text id="9e7h68"
The → cat → is → drinking → milk
                         ↓
                  [Context Vector]
                         ↓
                      Decoder
```

For short sequences, this could work reasonably well.

For long sequences, however, important information could be difficult to preserve in a single representation.

This created an **information bottleneck**.

## The Idea Behind Attention

Instead of relying only on one fixed context vector, the decoder can look at the encoder's representations of the input.

For example:

```text id="5ul5fr"
The   cat   is   drinking   milk
 ↓     ↓    ↓       ↓        ↓
0.05  0.70 0.05    0.10     0.10
       ███████
          ↓
        "kedi"
```

When generating the word `kedi`, the model may assign a larger attention weight to `cat`.

When generating another word, the attention weights can change.

```text id="pc0zwb"
The   cat   is   drinking   milk
 ↓     ↓    ↓       ↓        ↓
0.02  0.05 0.08    0.78     0.07
                    ████████
                        ↓
                     "içiyor"
```

The model can therefore focus on different parts of the input while generating different parts of the output.

## How Does Attention Work?

The encoder produces a representation for each input element.

```text id="33c1m7"
The       → h₁
cat       → h₂
is        → h₃
drinking  → h₄
milk      → h₅
```

When the decoder wants to generate the next output, the attention mechanism calculates a score for each encoder representation.

For example:

```text id="p2unvv"
h₁ → 0.05
h₂ → 0.70
h₃ → 0.05
h₄ → 0.10
h₅ → 0.10
```

These scores indicate how relevant each part of the input is for the current output step.

After normalization, the attention weights can be used to create a weighted context vector.

```text id="yxrm5g"
Context =

0.05 × h₁
+
0.70 × h₂
+
0.05 × h₃
+
0.10 × h₄
+
0.10 × h₅
```

The resulting context is then used by the decoder.

```text id="j5pg0m"
Encoder Representations

h₁   h₂   h₃   h₄   h₅
 \    |    |    |   /
  \   |    |   /   /
      Attention
          ↓
       Context
          ↓
       Decoder
          ↓
      Next Output
```

The attention weights are recalculated for each output step.

## Without Attention

```text id="3h6r8h"
Input Sequence
      ↓
    Encoder
      ↓
Fixed Context
      ↓
    Decoder
```

The decoder depends heavily on one compressed representation of the input.

## With Attention

```text id="br2y8l"
Input Representations
 ↓    ↓    ↓    ↓    ↓
      Attention
          ↓
Relevant Information
          ↓
       Decoder
          ↓
        Output
```

The decoder can access different parts of the encoded input as needed.

## Why Was Attention Important?

Attention helped neural networks handle longer sequences more effectively.

Instead of forcing all information through a single fixed-size representation, the model could dynamically select relevant information.

This became especially important for tasks such as:

- Machine translation
- Text generation
- Speech recognition
- Sequence modeling

## Attention vs Self-Attention

The attention mechanism used in early Seq2Seq systems should not be confused with **Self-Attention**.

In classic Encoder–Decoder attention:

```text id="dax9be"
Decoder
   ↓
looks at
   ↓
Encoder representations
```

With Self-Attention:

```text id="egb8j1"
Words in the same sequence
        ↓
attend to each other
```

For example:

```text id="uyhx83"
The animal didn't cross the street
because it was tired.
        ↑
        │
"it" can attend to "animal"
```

Self-Attention later became one of the central components of the **Transformer** architecture.

## What's Next?

Early attention mechanisms were commonly combined with RNN or LSTM-based Encoder–Decoder models.

Then, in 2017, a major question emerged:

> What if we built a sequence model around attention instead of relying on recurrent networks?

This led to the paper:

**Attention Is All You Need**

and the introduction of the **Transformer** architecture.

```text id="sm2abk"
RNN
 ↓
LSTM
 ↓
Seq2Seq
 ↓
Attention
 ↓
Self-Attention
 ↓
Transformer
```