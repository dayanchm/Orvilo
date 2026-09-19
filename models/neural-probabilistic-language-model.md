# Neural Probabilistic Language Model

## From Counting Words to Learning Representations

In 2003, **Yoshua Bengio, Réjean Ducharme, Pascal Vincent, and Christian Jauvin** introduced *A Neural Probabilistic Language Model*.

This work was an important step from traditional statistical language models toward neural language models.

## The Problem with N-grams

N-gram language models predict the next word by counting how often sequences of words appear in a dataset.

For example:

```text id="n55ds1"
I love Go
I love Python
I like Go
```

An n-gram model can calculate:

```text id="p0tjrp"
I love → Go      50%
I love → Python  50%
```

However, words are essentially treated as separate symbols.

For example:

```text id="wh1jqu"
cat
dog
car
```

The model does not naturally know that `cat` and `dog` are more semantically related than `cat` and `car`.

Another problem is that there are an enormous number of possible word sequences, while only a small fraction of them appear in the training data.

## The Neural Approach

Instead of relying only on counts, the neural probabilistic language model learns a numerical representation for each word.

```text id="w4nwhv"
Previous words

I   love   programming
↓     ↓         ↓

Learned word vectors

[0.2, 0.8, ...]
[0.7, 0.1, ...]
[0.4, 0.9, ...]

        ↓

  Neural Network

        ↓

      Softmax

        ↓

Next-word probabilities

Go      40%
Python  30%
C++     15%
...
```

These learned representations allow the model to capture similarities between words and generalize better to word sequences that may not have appeared exactly in the training data.

## How Does It Learn?

Suppose the training sentence is:

```text id="l18ywy"
I love programming in Go
```

The model receives the previous words:

```text id="6zwrkg"
I love programming in
```

The correct next word is:

```text id="5y0rzi"
Go
```

At the beginning of training, the model might predict:

```text id="jz8bmk"
Python  40%
Java    25%
Go       5%  ← correct word
...
```

The prediction is compared with the actual next word.

```text id="iwvql3"
Prediction
    ↓
Compare with correct word
    ↓
Calculate loss
    ↓
Backpropagation
    ↓
Update parameters
```

This process is repeated across many examples.

Over time, the model learns both:

- useful numerical representations of words
- neural network parameters for predicting the next word

## N-gram vs Neural Language Model

### N-gram

```text id="7h3hni"
Words
  ↓
Count occurrences
  ↓
Estimate probabilities
  ↓
Predict next word
```

### Neural Probabilistic Language Model

```text id="p4g9ke"
Words
  ↓
Learned word representations
  ↓
Neural Network
  ↓
Softmax
  ↓
Predict next word
```

The important transition is:

```text id="cj4fx3"
Counting patterns
       ↓
Learning representations and patterns
```

## Why Was It Important?

The neural probabilistic language model showed that a neural network could learn both **distributed representations of words** and a **probability distribution for the next word**.

The general idea is surprisingly familiar today:

```text id="h8d97z"
2003 Neural Language Model

Previous words
      ↓
Neural Network
      ↓
Next-word probabilities
```

Modern language models use much more advanced architectures:

```text id="yy9pm6"
Modern LLM

Previous tokens
      ↓
Transformer
      ↓
Next-token probabilities
```

The architecture changed dramatically, but predicting language through learned representations and probabilities remains a fundamental idea.

## What's Next?

The 2003 model still used a **fixed-size context**: only a limited number of previous words were given to the neural network.

The next major question was:

> What if the model could process a sequence while carrying information from previous words forward?

This leads us to **Recurrent Neural Networks (RNNs)**.