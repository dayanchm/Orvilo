# GPT

## Generative Pre-trained Transformer

**GPT** stands for **Generative Pre-trained Transformer**.

GPT is a family of language models based on the **Transformer** architecture.

Unlike the original Transformer architecture, which contained both an encoder and a decoder, GPT uses a **decoder-only Transformer** architecture.

The basic idea is:

```text id="ig2j7g"
Text
 ↓
Tokens
 ↓
Embeddings
 ↓
Transformer
 ↓
Next-token probabilities
 ↓
Generate next token
```

---

# GPT-1

## Generative Pre-Training

**GPT-1** was introduced by OpenAI in **2018** in the paper:

**Improving Language Understanding by Generative Pre-Training**

GPT-1 demonstrated that a Transformer language model could first learn general language patterns from a large amount of unlabeled text and then be adapted to different NLP tasks.

## The Main Idea

Before this approach, many NLP systems were trained specifically for individual tasks.

For example:

```text id="4bf67v"
Sentiment task
     ↓
Separate model

Question answering
     ↓
Separate model

Text classification
     ↓
Separate model
```

GPT explored a different approach:

```text id="kg81ji"
Large amount of text
        ↓
    Pre-training
        ↓
General language model
        ↓
    Fine-tuning
        ↓
Specific NLP task
```

This introduced two important stages:

1. **Pre-training**
2. **Fine-tuning**

## Pre-training

During pre-training, GPT learns by predicting the next token from previous tokens.

For example:

```text id="n8vbkb"
The cat is sitting on the ___
```

The model might predict:

```text id="qsc6j1"
floor    42%
chair    25%
table    14%
...
```

The goal is to increase the probability of the correct next token.

Conceptually:

```text id="48csxq"
Previous tokens
      ↓
     GPT
      ↓
Next-token probabilities
      ↓
Compare with correct token
      ↓
Loss
      ↓
Backpropagation
      ↓
Update parameters
```

This process is repeated across a large text dataset.

## Autoregressive Language Modeling

GPT predicts tokens from left to right.

```text id="rj79rm"
I
↓
I love
↓
I love programming
↓
I love programming in
↓
I love programming in Go
```

Mathematically, the idea can be written as:

```text id="ym9nr7"
P(x₁, x₂, ..., xₙ)

=

P(x₁)
× P(x₂ | x₁)
× P(x₃ | x₁, x₂)
× ...
× P(xₙ | x₁, ..., xₙ₋₁)
```

In simple terms:

> Predict the next token using all previous tokens.

## Architecture

GPT-1 uses a **decoder-only Transformer**.

A simplified pipeline:

```text id="bzy1l8"
Input Text
    ↓
Tokenization
    ↓
Token Embeddings
    +
Position Embeddings
    ↓
Transformer Blocks
    ↓
Final Representations
    ↓
Output Probabilities
```

The Transformer uses **masked self-attention**.

## Masked Self-Attention

When predicting a token, the model must not see future tokens.

Suppose the training sentence is:

```text id="x9u6s6"
I love programming in Go
```

When processing:

```text id="rvkyid"
I love programming
```

the model can attend to:

```text id="52gz8h"
I
love
programming
```

but it cannot look ahead at:

```text id="2r9ksn"
in
Go
```

Conceptually:

```text id="1msx2c"
I       ← can see I
love    ← can see I, love
program ← can see I, love, program
in      ← can see everything before "in"
Go      ← can see everything before "Go"
```

This is called **causal** or **masked self-attention**.

## Fine-Tuning

After pre-training, GPT-1 could be adapted to specific tasks using labeled datasets.

```text id="km2xsk"
       Pre-trained GPT
             ↓
     ┌───────┼────────┐
     ↓       ↓        ↓
Sentiment    QA    Classification
```

Instead of learning language from scratch for every task, the model could reuse what it learned during pre-training.

## GPT-1 Size

GPT-1 had approximately:

```text id="8d7bmt"
117 million parameters
```

and used:

```text id="l2w3ay"
12 Transformer layers
```

By modern LLM standards this is small, but at the time it demonstrated an important approach.

## Why Was GPT-1 Important?

GPT-1 helped demonstrate a powerful idea:

```text id="r9tcez"
Learn language first
        ↓
Then adapt that knowledge
to different tasks
```

Instead of building a completely new model for every NLP problem:

```text id="0a6qqp"
Large unlabeled text
        ↓
General pre-training
        ↓
Reusable language model
        ↓
Different downstream tasks
```

This became an important foundation for later GPT models.

---

# GPT-2

## Language Models as Unsupervised Multitask Learners

**GPT-2** was introduced by OpenAI in **2019** in the technical report:

**Language Models are Unsupervised Multitask Learners**

GPT-2 kept the main idea and decoder-only architecture of GPT-1, but increased
the model size and trained on a larger, more varied collection of web text.

The central question changed from:

> Can one pre-trained model be fine-tuned for many tasks?

to:

> Can a language model begin to perform different tasks without being explicitly
> trained for each one?

## From Fine-Tuning to Zero-Shot Learning

GPT-1 usually followed this process:

```text
Pre-train on general text
          ↓
Fine-tune on labeled examples for one task
          ↓
Perform that task
```

GPT-2 showed early evidence of a different process:

```text
Pre-train on many kinds of text
          ↓
Describe or demonstrate a task in the input
          ↓
Continue the text in a way that performs the task
```

This is called **zero-shot learning** when the model is evaluated on a task
without task-specific training examples or parameter updates.

For example, a prompt can turn translation into text completion:

```text
English: Hello, how are you?
French:
```

The model still performs its usual operation—predicting the next token—but the
text before the prediction tells it what kind of continuation is expected.

## WebText

GPT-2 was trained on **WebText**, a dataset created from links shared on Reddit
that received at least three karma. The linked pages were collected and cleaned,
with Wikipedia pages removed to reduce overlap with common evaluation data.

The resulting dataset contained text from roughly:

```text
8 million web pages
```

Using varied web pages mattered because natural text already contains many
examples of tasks:

```text
Questions followed by answers
Articles followed by summaries
Sentences followed by translations
Instructions followed by solutions
```

By learning to predict continuations across this mixture, GPT-2 could acquire
some task behavior without a separate labeled dataset for every task.

## Architecture and Size

The largest GPT-2 model had approximately:

```text
1.5 billion parameters
48 Transformer layers
1,024-token context window
```

It was more than ten times larger than GPT-1 by parameter count.

```text
GPT-1                         GPT-2
117 million parameters   →   1.5 billion parameters
12 layers                →   48 layers
```

GPT-2 used **byte-level byte pair encoding**, a subword tokenization method.
Instead of requiring a fixed vocabulary containing every possible word, it could
represent text using reusable token pieces and bytes.

## Text Generation

GPT-2 could generate a long continuation from a short prompt:

```text
Prompt
  ↓
Tokenize the prompt
  ↓
Predict a probability distribution for the next token
  ↓
Select one token
  ↓
Append it to the prompt
  ↓
Repeat
```

Sampling settings affect the result. Always selecting the most probable token
can make text repetitive, while sampling from several likely tokens can produce
more varied output.

## What GPT-2 Demonstrated

GPT-2 showed that increasing model capacity and training-data diversity could
improve both generation and task-general behavior.

It displayed zero-shot ability on tasks such as:

- Question answering
- Reading comprehension
- Summarization
- Translation

These abilities were incomplete and inconsistent, but they suggested that tasks
could sometimes be represented through ordinary text rather than through a new
model architecture or a separate training procedure.

## Staged Release

OpenAI initially released smaller GPT-2 versions rather than the full model,
citing concerns about possible misuse of generated text. The 1.5-billion-
parameter version was released later in 2019 after a staged release process.

This made GPT-2 notable not only for its technical results, but also for an early
public discussion about how powerful generative models should be released.

## Limitations of GPT-2

GPT-2 did not understand or verify claims in the human sense. Its objective was
to produce a probable continuation.

As a result, it could:

- State false information confidently
- Lose coherence over a long passage
- Repeat phrases or ideas
- Reflect biases and harmful patterns in web data
- Produce different answers when a prompt was phrased differently

Fluent text is therefore not the same as factual or reliable text.

## Why Was GPT-2 Important?

GPT-2 helped connect language modeling with general task performance:

```text
More diverse data
       +
Larger decoder-only Transformer
       +
Next-token prediction
       ↓
Better generation and emerging zero-shot abilities
```

Its results led naturally to another question:

> How far can this approach go if the model and training computation are scaled
> much further?

That question led to **GPT-3**.

---

# GPT-3

## Language Models as Few-Shot Learners

**GPT-3** was introduced by OpenAI in **2020** in the paper:

**Language Models are Few-Shot Learners**

GPT-3 was not based on a completely new language-modeling objective. Like GPT-1
and GPT-2, it was an autoregressive, decoder-only Transformer trained to predict
the next token.

Its defining change was scale.

## GPT-3 Size

The largest GPT-3 model had:

```text
175 billion parameters
96 Transformer layers
2,048-token context window
```

OpenAI trained eight GPT-3 model sizes, from **125 million** to **175 billion**
parameters, to study how performance changed as models became larger.

```text
GPT-1           GPT-2             GPT-3
117M       →    1.5B        →     175B parameters
```

The largest GPT-3 had more than 100 times as many parameters as the largest
GPT-2.

## Training Data

GPT-3 was trained on a mixture of sources, including:

- Filtered Common Crawl web pages
- WebText-style data
- Two internet-based book collections
- English-language Wikipedia

The sources were filtered, deduplicated, and sampled with different weights.
The paper reports that the model processed about **300 billion tokens** during
training.

The training objective remained simple:

```text
Previous tokens
      ↓
Decoder-only Transformer
      ↓
Probability of every possible next token
      ↓
Increase the probability of the actual next token
```

## In-Context Learning

GPT-3's most influential result was **in-context learning**.

The model could sometimes infer a task from instructions or examples placed in
the prompt. Its parameters were not updated during this process.

```text
Task instruction + optional examples + new input
                       ↓
                One text prompt
                       ↓
                     GPT-3
                       ↓
                    Completion
```

This is different from fine-tuning:

```text
Fine-tuning
Examples → training → parameter updates → adapted model

In-context learning
Examples → prompt → no parameter updates → immediate completion
```

The examples are temporary context. They guide the current prediction but do not
permanently teach or modify the model.

## Zero-Shot, One-Shot, and Few-Shot

The GPT-3 paper evaluated three main settings.

### Zero-Shot

The prompt contains an instruction and the input, but no completed example.

```text
Translate English to French:

English: Good morning
French:
```

### One-Shot

The prompt contains one completed example before the new input.

```text
English: Thank you
French: Merci

English: Good morning
French:
```

### Few-Shot

The prompt contains several completed examples.

```text
English: Thank you
French: Merci

English: Goodbye
French: Au revoir

English: Good morning
French:
```

These settings do not mean that GPT-3 was trained from scratch using zero, one,
or a few examples. The model had already completed large-scale pre-training. The
terms describe how many task examples were supplied in the prompt at evaluation
time.

## Why Examples in the Prompt Help

An example communicates more than its individual answer. It also shows the model:

- What task to perform
- What input and output format to use
- Which pattern connects input to output
- What style the answer should follow

Conceptually:

```text
Example 1 ─┐
Example 2 ─┼─→ infer the pattern → complete the new case
Example 3 ─┘
```

As model scale increased, this behavior generally became more effective. GPT-3
could perform various language tasks through text interaction without a separate
gradient update for each task.

## What GPT-3 Could Do

The paper evaluated GPT-3 on tasks including:

- Question answering
- Translation
- Reading comprehension
- Cloze and completion tasks
- Simple arithmetic
- Word manipulation
- Generating articles and other passages

Performance varied substantially between tasks. GPT-3 was strong on some
benchmarks but weak on others, especially tasks requiring exact multi-step
reasoning, reliable arithmetic, or robust common-sense understanding.

## Prompt Sensitivity

Because the task is communicated through context, prompt design matters.

Small changes can affect the output:

```text
Instruction wording
Example order
Example formatting
Choice of examples
Amount of context
        ↓
Different probability distribution
        ↓
Different answer
```

This helped establish **prompting** as a practical way to interact with large
language models, while also revealing that their behavior could be unstable.

## Limitations of GPT-3

GPT-3's scale improved many capabilities, but did not make the model consistently
truthful, unbiased, or logically reliable.

Important limitations included:

- Hallucinating plausible but false information
- Weakness on some reasoning and arithmetic tasks
- Sensitivity to prompt wording and examples
- Reproducing social biases found in training data
- Difficulty distinguishing truth from a statistically likely continuation
- High computation and energy requirements for training and use
- Possible overlap between web training data and evaluation data

GPT-3 was also a **base model**, not yet the instruction-following assistant style
that later became familiar through InstructGPT and ChatGPT.

## Why Was GPT-3 Important?

GPT-3 showed that scaling a general next-token predictor could produce stronger
task-independent behavior and in-context learning.

```text
GPT-1
Pre-train, then fine-tune for each task
        ↓
GPT-2
Some tasks emerge in a zero-shot setting
        ↓
GPT-3
Tasks described with instructions and in-context examples
```

This did not eliminate fine-tuning, but it introduced a powerful additional way
to use language models: specify a task inside the prompt.

---

# GPT-1, GPT-2, and GPT-3 Compared

| Model | Year | Largest version | Main emphasis |
|---|---:|---:|---|
| GPT-1 | 2018 | 117 million parameters | General pre-training followed by task-specific fine-tuning |
| GPT-2 | 2019 | 1.5 billion parameters | Scaling and early zero-shot multitask behavior |
| GPT-3 | 2020 | 175 billion parameters | In-context zero-shot, one-shot, and few-shot learning |

The progression was not simply about generating better text. It changed how a
single model could be adapted to a task:

```text
GPT-1: update the model's parameters for the task
GPT-2: phrase some tasks as text completion
GPT-3: describe or demonstrate many tasks inside the prompt
```

All three models shared the same foundation:

```text
Decoder-only Transformer
          +
Causal self-attention
          +
Autoregressive next-token prediction
```

Their history illustrates a central lesson of modern language modeling: the same
basic learning objective can produce qualitatively new behavior when combined
with more model capacity, more data, and more computation.

## Sources

- [Improving Language Understanding by Generative Pre-Training](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)
- [Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)
- [Better Language Models and Their Implications](https://openai.com/index/better-language-models/)
- [Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165)
- [GPT-3 Model Card](https://github.com/openai/gpt-3/blob/master/model-card.md)
