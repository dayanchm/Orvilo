# N-gram Language Models

The easiest way to understand an n-gram language model is this: it predicts the next word based on how often sequences of words appear in a dataset.

## What is an N-gram?

An **n-gram** is a sequence of `N` consecutive words (or tokens).

For example, consider this small dataset:

```text
I love Go
I love programming
I love Go
I like Python
```

### Unigram (N=1)

A unigram contains one word.

```text
I            4
love         3
Go           2
programming  1
like         1
Python       1
```

### Bigram (N=2)

A bigram contains two consecutive words.

```text
I love             3
love Go            2
love programming   1
I like             1
like Python        1
```

### Trigram (N=3)

A trigram contains three consecutive words.

```text
I love Go            2
I love programming   1
I like Python         1
```

These counts can then be used to estimate the probability of what word might come next.

For example:

```text
I love ___
```

In our dataset:

```text
I love Go            → 2 times
I love programming   → 1 time
```

So a simple trigram model would estimate:

```text
P(Go | I love)           = 2/3 ≈ 67%
P(programming | I love)  = 1/3 ≈ 33%
```

The basic idea is:

```text
Previous words
      ↓
Count occurrences
      ↓
Calculate probabilities
      ↓
Predict the next word
```