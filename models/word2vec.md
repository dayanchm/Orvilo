# Word2Vec

## Learning Word Representations

**Word2Vec** was introduced by **Tomas Mikolov and colleagues in 2013**.

Word2Vec is not a language model like modern LLMs. It is a family of techniques used to learn numerical representations of words called **word embeddings**.

The main idea is simple:

> Words that appear in similar contexts should have similar representations.

## From Words to Vectors

Computers do not understand words directly.

Word2Vec represents each word as a vector of numbers.

```text id="7nj3sk"
cat → [ 0.21,  0.73, -0.14, ...]
dog → [ 0.25,  0.69, -0.10, ...]
car → [-0.81,  0.12,  0.54, ...]
```

If `cat` and `dog` frequently appear in similar contexts, their vectors may become closer to each other than to unrelated words such as `car`.

```text id="f9l9nw"
cat ●
     \
      ● dog


                         ● car
```

This numerical space is called an **embedding space**.

## How Does Word2Vec Learn?

Word2Vec learns word representations by solving simple prediction tasks.

There are two main architectures:

- **CBOW — Continuous Bag of Words**
- **Skip-gram**

## CBOW

CBOW tries to predict a target word using the words around it.

For example:

```text id="pcn9sl"
The ___ is drinking milk
```

The context is:

```text id="8gsbke"
The
is
drinking
milk
```

The model tries to predict:

```text id="7bgsmk"
cat
```

The basic idea is:

```text id="g8ow4v"
Context words
     ↓
   Word2Vec
     ↓
 Target word
```

Or:

```text id="1uuwvf"
"The" + "is" + "drinking" + "milk"
                 ↓
               CBOW
                 ↓
               "cat"
```

## Skip-gram

Skip-gram works in the opposite direction.

Instead of using the surrounding words to predict the target word, it uses the target word to predict words that may appear around it.

```text id="t0vj5s"
          drinking
             ↑
The  ←     cat     →  is
             ↓
            milk
```

The basic idea is:

```text id="4a3u8f"
Target word
     ↓
  Word2Vec
     ↓
Context words
```

## What Does the Model Learn?

Imagine the training data contains sentences such as:

```text id="hj1tnn"
the cat drinks water
the dog drinks water

the cat eats food
the dog eats food

the cat is an animal
the dog is an animal
```

`cat` and `dog` repeatedly appear in similar contexts.

During training, Word2Vec adjusts their numerical representations.

Eventually:

```text id="wq74qf"
vector(cat) ≈ vector(dog)
```

Their vectors become relatively close in the embedding space.

## Relationships Between Words

Word embeddings can also capture some relationships between words.

A famous example is:

```text id="8n6s0t"
king - man + woman ≈ queen
```

This does not mean Word2Vec understands these concepts like a human.

Instead, relationships that occur in the training data can appear as geometric patterns in the learned vector space.

## Why Was Word2Vec Important?

Word representations existed before Word2Vec.

For example, the **2003 Neural Probabilistic Language Model** already learned distributed representations of words.

Word2Vec's major contribution was providing simple and computationally efficient methods for learning useful word embeddings from large amounts of text.

The important transition can be thought of as:

```text id="ol08g3"
Word
 ↓
Learn from its context
 ↓
Vector
 ↓
Position in embedding space
```

Instead of treating words only as independent symbols:

```text id="8cr7fx"
cat ≠ dog ≠ car
```

we can represent relationships between them:

```text id="t90rqk"
cat ── close ── dog

car ─────────── farther away
```

## Word2Vec vs Language Models

Word2Vec primarily learns **word representations**.

```text id="ik0m4q"
Word
 ↓
Word2Vec
 ↓
Embedding
```

A language model predicts language:

```text id="z2m4m6"
Previous words
      ↓
Language Model
      ↓
Next-word probabilities
```

Modern language models still use embeddings, but they combine them with much more powerful architectures such as the **Transformer**.

## What's Next?

Word2Vec gives us a way to represent words as meaningful numerical vectors.

But language is a **sequence**.

The meaning of a word can depend heavily on the words that came before it.

This leads to another question:

> How can a neural network process a sequence while remembering information from previous steps?

This brings us to **Recurrent Neural Networks (RNNs)**.