# LSTM

LSTM (1997) is not a model by itself, but a type of recurrent neural network architecture designed for processing sequential data.

## What is an LSTM?

**LSTM = Long Short-Term Memory**

It was introduced by **Sepp Hochreiter and Jürgen Schmidhuber in 1997**.

LSTM was developed to address a major problem in traditional Recurrent Neural Networks (RNNs): learning long-term dependencies.

## First: What is an RNN?

An RNN processes a sequence step by step while carrying information from previous steps.

```text id="2j3e9y"
I → love → programming → in → Go
    ─────────────────────→
       information flows forward
```

Unlike a basic neural network, an RNN has a **hidden state** that acts like a memory of previous inputs.

```text id="t81j6c"
word₁ → RNN → hidden state₁
                  ↓
word₂ → RNN → hidden state₂
                  ↓
word₃ → RNN → hidden state₃
```

## The Problem with RNNs

Traditional RNNs can struggle to learn relationships between information that is far apart in a sequence.

For example:

```text id="gjx65b"
The dog that I saw in the park yesterday was ___
```

To predict the next word correctly, information about **"dog"** may still be important even though several words have appeared since then.

During training, standard RNNs can suffer from problems such as the **vanishing gradient**, making long-term dependencies difficult to learn.

## How Does LSTM Help?

LSTM introduces a special memory called the **cell state**.

```text id="mpt3f7"
Input
  ↓
LSTM
  ├── Hidden State
  └── Cell State  ← long-term information
```

LSTM uses **gates** to control the flow of information.

There are three main gates:

```text id="1mmrgp"
Forget Gate
    ↓
What should I forget?

Input Gate
    ↓
What new information should I store?

Output Gate
    ↓
What information should I output?
```

This allows the network to learn what information should be remembered, updated, or forgotten as it processes a sequence.

## LSTM as a Language Model

LSTM itself is an architecture, but it can be used to build a language model.

```text id="7rzx68"
Words
  ↓
Embeddings
  ↓
LSTM
  ↓
Linear Layer
  ↓
Softmax
  ↓
Next-word probabilities
```

For example:

```text id="75ny6s"
Input:

"I love programming in"

        ↓
      LSTM
        ↓

Go       40%
Python   30%
Rust     15%
...
```

The language model can use information from previous words to predict the next word.

## Why Was LSTM Important?

LSTM made it easier for neural networks to learn longer-term patterns in sequential data.

It became widely used for tasks involving sequences, including:

- Language modeling
- Machine translation
- Speech recognition
- Text generation

Later, architectures based on **attention** and **Transformers** became dominant for many language-modeling tasks.