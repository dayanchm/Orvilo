# Embeddings During Model Training

An embedding layer maps each token ID to a learned vector. These vectors are the model's initial numeric representation of tokens and are updated with the rest of the network during training.

This guide covers internal model embeddings. For retrieval embeddings, see the separate [RAG embeddings guide](../rag/embeddings.md).

## Embedding Lookup

~~~mermaid
flowchart LR
    T["Token: cat"] --> I["ID: 4812"]
    I --> M[("Embedding matrix<br/>vocabulary × hidden size")]
    M --> V["Dense vector"]
    P["Position information"] --> A["Combined representation"]
    V --> A
    A --> TR["Transformer layers"]
~~~

Looking up a token selects one row of the embedding matrix. Similar usage can cause token vectors to develop related directions, but individual dimensions usually do not have simple human meanings.

## Token and Position Information

Token embeddings identify content. Position methods tell the model where tokens occur.

| Position method | Basic idea |
|---|---|
| Learned absolute | Add a trained vector for each position |
| Sinusoidal | Add deterministic periodic features |
| RoPE | Rotate query and key features by position |
| Relative bias | Add attention bias based on distance |
| ALiBi | Penalize attention according to distance |

Position design affects length generalization and context extension.

## Input and Output Weights

A language model converts final hidden states into vocabulary logits. Some architectures **tie** the output matrix to the input embedding matrix, reducing parameters and sharing the learned token space.

The softmax over logits produces next-token probabilities.

## How Embeddings Learn

If the model assigns low probability to the correct next token, backpropagation computes how each active embedding contributed to the error. The optimizer adjusts the selected token rows and all later layers.

Frequent tokens receive many updates. Rare tokens depend more on shared subword pieces and generalization.

## Embedding Space Is Context-Free at Input

The initial token vector is the same wherever that token appears. Transformer layers turn it into a contextual hidden state. “Bank” in “river bank” and “bank account” starts from the same token embedding but develops different contextual representations.

## Vocabulary Expansion

Adding tokens after pretraining adds untrained embedding rows and often output rows. Initialize them from related token pieces, then continue training. A new token does not automatically carry the meaning of its text label.

Changing token IDs without matching the embedding matrix corrupts the model.

## Evaluation

Inspect language fertility, rare-token behavior, nearest neighbors, representation anisotropy, and downstream task quality. Avoid interpreting nearest neighbors as proof of a model's beliefs.

## Related Guides

- [Tokenization](tokenization.md)
- [Loss Functions](loss-functions.md)
- [Backpropagation](backpropagation.md)
