# Vector Search

Vector search finds indexed items whose embeddings are closest to a query embedding. It turns semantic similarity into a practical retrieval operation over large collections.

## Search Flow

~~~mermaid
flowchart LR
    Q["Question"] --> E["Query embedding"]
    E --> I[("Vector index")]
    F["Metadata filters"] --> I
    I --> K["Top-k candidates"]
    K --> R["Retriever or reranker"]
~~~

## Exact and Approximate Search

Exact nearest-neighbor search compares the query with every vector. It is simple and accurate but becomes expensive as the collection grows.

Approximate nearest-neighbor (**ANN**) indexes trade a small amount of recall for much faster search.

| Method | Idea | Tradeoff |
|---|---|---|
| Flat search | Compare every vector | Exact but slow at scale |
| HNSW | Navigate a layered proximity graph | Strong recall; memory-heavy |
| IVF | Search selected vector clusters | Tunable speed and recall |
| Product quantization | Compress vector components | Lower memory; lower precision |
| Disk-based ANN | Optimize graph or clusters for disk | Larger scale; storage latency |

Index parameters must be tuned with real queries. Faster search is not useful if answer-bearing chunks disappear.

## Metadata Filtering

Vector similarity alone cannot enforce requirements such as tenant, language, region, product version, effective date, or access group.

~~~text
search(
  query_vector,
  filter = {
    tenant_id: "acme",
    access_groups: ["employees"],
    effective_at: { before_or_equal: today }
  },
  top_k = 20
)
~~~

Apply authorization inside or before search. Retrieving forbidden content and hiding it only after generation is a data leak.

## Top-k

A small k reduces latency and noise but may miss evidence. A large k increases recall while adding duplicate or irrelevant candidates.

A common design retrieves a wider candidate set and lets a reranker choose a smaller context set. Tune both values using recall, downstream answer quality, and latency.

## Hybrid Search

~~~text
hybrid_score =
    alpha * normalized_dense_score
  + (1 - alpha) * normalized_sparse_score
~~~

Hybrid search combines semantic dense retrieval with lexical search such as BM25. Scores from different systems need normalization or rank fusion; their raw scales are usually incompatible.

Reciprocal Rank Fusion combines ranks without assuming comparable scores.

## Index Operations

Production indexes need upsert, delete, namespace or tenant isolation, filtering, backups, replication, and versioned migration. Monitor index lag so users know how quickly source changes become searchable.

Avoid duplicate chunk IDs and stale vectors after a document update.

## Common Failures

- using the wrong distance metric;
- mixing vectors from different embedding models;
- omitting metadata filters;
- choosing k without evaluation;
- indexing duplicate or empty chunks;
- assuming an ANN index has perfect recall;
- exposing similarity score as confidence.

## Evaluation

Compare ANN results with exact search on a sample to measure index recall. Separately measure relevance with labeled queries. Monitor latency percentiles, filter selectivity, storage size, update delay, and result diversity.

## Related Guides

- [Embeddings](embeddings.md)
- [Retrieval](retrieval.md)
- [Reranking](reranking.md)
