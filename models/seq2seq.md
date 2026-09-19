# Seq2Seq

## Sequence to Sequence

**Seq2Seq** stands for **Sequence to Sequence**.

Seq2Seq became an important neural network approach in **2014**, particularly for tasks such as machine translation.

The basic idea is simple:

> Take one sequence as input and produce another sequence as output.

For example:

```text id="3rwyg8"
Input:
How are you?

      ↓

   Seq2Seq

      ↓

Output:
Nasılsın?
```

The input and output sequences do not need to have the same length.

## Why Do We Need Seq2Seq?

A traditional language model often focuses on predicting the next word:

```text id="b6f6wm"
Previous words
      ↓
Language Model
      ↓
Next word
```

But some problems require transforming an entire sequence into another sequence.

For example, machine translation:

```text id="k0y5mm"
"I love programming"
         ↓
      Seq2Seq
         ↓
"Programlamayı seviyorum"
```

This led to the **Encoder–Decoder** architecture.

## Encoder

The encoder processes the input sequence step by step.

In early Seq2Seq systems, the encoder was commonly built using recurrent neural networks such as **LSTMs**.

```text id="clu9pt"
I → love → programming
         ↓
      Encoder
         ↓
   Representation
```

The encoder's job is to transform the input sequence into an internal representation.

## Decoder

The decoder receives the representation created by the encoder and generates the output sequence step by step.

```text id="8g1jlu"
Representation
      ↓
   Decoder
      ↓
Programlamayı
      ↓
seviyorum
      ↓
    <END>
```

The complete process looks like this:

```text id="kqlopk"
"I love programming"

         ↓

      ENCODER
       (LSTM)

         ↓

   Context Vector

         ↓

      DECODER
       (LSTM)

         ↓

"Programlamayı seviyorum"
```

## How Does Generation Work?

The decoder does not usually generate the entire sentence at once.

It generates one token at a time.

```text id="m8u86u"
Context
   ↓
"Programlamayı"
   ↓
"seviyorum"
   ↓
<END>
```

Each generated token can be used as part of the input for generating the next token.

```text id="5t0d5a"
<START>
   ↓
Programlamayı
   ↓
seviyorum
   ↓
<END>
```

## The Problem

Early Seq2Seq models had an important limitation.

The encoder attempted to compress the input sequence into a **fixed-size context vector**.

```text id="2cpbdg"
Input sequence

The → dog → that → I → saw → yesterday → ...

                    ↓

                 Encoder

                    ↓

            [ Context Vector ]

                    ↓

                 Decoder
```

For short sequences, this could work reasonably well.

For longer sequences, important information could be difficult to preserve in a single fixed-size representation.

This created an **information bottleneck**.

```text id="h44wvn"
Large amount of information
            ↓
         Encoder
            ↓
     [ one context ]
            ↓
         Decoder
```

## Why Was Seq2Seq Important?

Seq2Seq provided a powerful general framework for mapping one variable-length sequence to another.

It became useful for tasks such as:

- Machine translation
- Text generation
- Speech recognition
- Question answering
- Conversational systems

Most importantly, its limitations helped motivate the development of a major new idea.

## What's Next?

Instead of forcing the decoder to rely only on one fixed context vector, what if the decoder could look back at different parts of the input while generating each output?

```text id="2e8a37"
Input words
↓   ↓   ↓   ↓
Encoder states
 \  |  /  /
  \ | /  /
 ATTENTION
     ↓
  Decoder
     ↓
Next output
```

This idea became known as **Attention**.

The progression is:

```text id="h4cdl9"
RNN
 ↓
LSTM
 ↓
Seq2Seq
 ↓
Attention
 ↓
Transformer
```