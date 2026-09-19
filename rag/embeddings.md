# Embeddings

An embedding model converts text, images, or other data into numeric vectors. Items with related meaning should occupy nearby regions of the vector space, allowing semantic search beyond exact keyword matching.

## From Text to Vector

~~~mermaid
flowchart LR
    T["Annual leave is 20 days"] --> M["Embedding model"]
    M --> V["[0.12, -0.08, 0.44, …]"]
    Q["How much vacation do I get?"] --> M
    M --> QV["[0.10, -0.05, 0.41, …]"]
    V -. "nearby" .- QV
~~~

The words “vacation” and “annual leave” differ, but their vectors can still be similar.

## Document and Query Embeddings

Some models use the same encoder for both sides. Others distinguish query and document modes with different prefixes or encoders. Follow the model's documented input format; using the wrong mode can reduce retrieval quality.

Normalize text consistently, but do not remove domain symbols or identifiers that users search for.

## Choosing an Embedding Model

| Dimension | Question |
|---|---|
| Retrieval quality | Does it find answer-bearing passages on your data? |
| Language coverage | Does it support every required language? |
| Domain | Does it represent legal, medical, code, or product terminology? |
| Dimensions | What are the storage and search costs per vector? |
| Input limit | Can it encode the selected chunk sizes? |
| Latency | Can indexing and queries meet service targets? |
| Deployment | Hosted API, private cloud, or local? |
| Versioning | Can the exact model and configuration be pinned? |

Leaderboard performance is a starting point, not a substitute for evaluation on real queries.

## Similarity

Cosine similarity compares vector direction:

~~~text
cosine(q, d) = (q · d) / (||q|| × ||d||)
~~~

Dot product and Euclidean distance are also common. The correct metric depends on how the embedding model was trained and whether vectors are normalized.

Similarity scores are not calibrated probabilities. A score of 0.8 does not mean an 80% chance of relevance.

## Indexing Example

~~~text
for each document:
    chunks = split(document)
    for each chunk:
        vector = embed_document(chunk.text)
        index.upsert(
            id=chunk.id,
            vector=vector,
            metadata=chunk.metadata
        )
~~~

Store the source text or a reliable text-store reference alongside the vector. A vector alone cannot produce a citation.

## Model Changes

Vectors from different embedding spaces are generally not comparable. When changing model, dimensions, normalization, or prefixes:

1. create a versioned index;
2. re-embed the corpus;
3. evaluate old and new indexes;
4. switch traffic safely;
5. retire old vectors after rollback is no longer needed.

Record the embedding model version on every indexed item.

## Dense and Sparse Representations

Dense embeddings capture semantic similarity. Sparse representations such as BM25 preserve exact terms and rare identifiers. Hybrid retrieval often performs better because “vacation policy” benefits from semantics while an error code such as HR-2047 needs lexical matching.

## Risks and Privacy

Hosted embedding APIs may receive sensitive text. Review retention and training policies, minimize personal data, and enforce regional requirements. Embeddings can leak information and must be protected like derived document data.

## Evaluation

Measure retrieval recall and ranking quality, not whether vectors “look reasonable.” Test synonyms, exact IDs, negation, multilingual questions, short queries, and domain-specific terminology.

## Further Reading

- [Sentence-BERT](https://arxiv.org/abs/1908.10084)
- [Dense Passage Retrieval](https://arxiv.org/abs/2004.04906)
