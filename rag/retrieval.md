# Retrieval

Retrieval selects evidence for a question. It includes more than vector search: query transformation, authorization, candidate generation, filtering, deduplication, diversity, and context assembly all affect what the generator sees.

## Retrieval Pipeline

~~~mermaid
flowchart LR
    Q["User question"] --> U["Understand / rewrite"]
    U --> D["Dense search"]
    U --> S["Sparse search"]
    D --> F["Fuse candidates"]
    S --> F
    F --> A["Access + metadata filters"]
    A --> X["Deduplicate / diversify"]
    X --> R["Rerank"]
    R --> C["Context set"]
~~~

## Query Transformation

A user's wording may not match the corpus. Transformations include:

- spelling or acronym normalization;
- converting conversation context into a standalone question;
- generating multiple query perspectives;
- extracting exact entities and filters;
- creating a hypothetical answer for embedding;
- translating the query for a multilingual corpus.

Keep the original intent. Over-aggressive rewriting can replace the user's question with a different one.

## Dense, Sparse, and Hybrid Retrieval

| Method | Strong at | Weak at |
|---|---|---|
| Dense | Paraphrases and semantic similarity | Exact rare identifiers |
| Sparse / BM25 | Names, codes, quotations, keywords | Vocabulary mismatch |
| Hybrid | Mixed natural-language and exact queries | More tuning and infrastructure |
| Structured lookup | Dates, prices, permissions, known keys | Open-ended semantic questions |
| Graph traversal | Relationships and multi-hop links | Corpus construction complexity |

A production retriever can route parts of a query to different sources rather than forcing every question through one vector index.

## Multi-Query Retrieval

For “Can unused vacation be moved to next year?”, generate variations such as “annual leave carry-over policy” and “rollover unused leave.” Search each, combine results, and remove duplicates.

Multi-query improves recall but costs more and can drift. Evaluate the generated queries and cap their number.

## Context Assembly

The highest-scoring chunks are not always the best set. The answer may require a definition from one section and an exception from another.

Context assembly may:

- merge adjacent chunks from the same document;
- retrieve the parent section of a matched child;
- favor diverse documents;
- remove near duplicates;
- order passages by source structure;
- fit the final selection within a token budget.

## Authorization and Freshness

Filter by user and tenant permissions before text is returned. Respect effective dates, superseded versions, legal holds, and deletion.

Caches must include authorization and index-version information in their keys. Otherwise one user's result can leak to another or stale content can survive an update.

## Confidence and Abstention

Similarity is not evidence sufficiency. Build an abstention rule from retrieval features and labeled data: relevant result count, reranker margin, source authority, contradiction, and whether retrieved text contains the required answer.

A safe response can say that the knowledge base does not contain enough information.

## Retrieval Example

Question: “Can I carry unused leave into next year?”

Good candidate set:

1. Annual Leave → Carry-over: up to five days.
2. Annual Leave → Eligibility: full-time employees.
3. Annual Leave → Expiration: carried days expire after one year.

The Remote Work Policy should not consume context merely because it also discusses employee eligibility and approval.

## Evaluation

Use a labeled set of queries and answer-bearing chunk IDs. Measure Recall@k, Precision@k, Mean Reciprocal Rank, nDCG, source diversity, authorization correctness, and latency. Include no-answer and adversarial queries.

## Further Reading

- [Dense Passage Retrieval](https://arxiv.org/abs/2004.04906)
- [BEIR: A Heterogeneous Benchmark for Information Retrieval](https://arxiv.org/abs/2104.08663)
