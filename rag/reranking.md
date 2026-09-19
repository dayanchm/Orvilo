# Reranking

Reranking uses a more precise model or scoring method to reorder a small candidate set returned by a fast retriever. Retrieval maximizes recall; reranking improves precision before evidence reaches the generator.

## Two-Stage Search

~~~mermaid
flowchart LR
    Q["Question"] --> R["Fast retrieval<br/>top 50"]
    I[("Index")] --> R
    R --> X["Reranker"]
    X --> K["Best 5 passages"]
    K --> G["Generator"]
~~~

It is usually too expensive to run a powerful reranker over every chunk, so a cheap search stage narrows the collection first.

## Reranker Types

| Type | How it scores | Strength | Cost |
|---|---|---|---|
| Cross-encoder | Reads query and passage together | Strong semantic precision | One inference per pair or batch |
| Late interaction | Compares token-level representations | Good quality and reusable document vectors | Larger index |
| LLM listwise | Orders several passages in a prompt | Flexible, can use instructions | High latency and variability |
| Rule-based | Uses metadata, freshness, authority | Predictable and auditable | Limited semantic judgment |
| Learned ranker | Combines many retrieval features | Tunable to product goals | Needs training data |

## Pairwise and Listwise Ranking

A pointwise or cross-encoder reranker scores each query–passage pair. A listwise reranker sees several candidates and orders them together. Listwise comparison can improve relative judgment but must handle order bias and context limits.

## Features Beyond Relevance

The best source is not only semantically similar. Ranking can incorporate:

- source authority;
- document freshness and effective date;
- product or jurisdiction match;
- user permissions;
- passage completeness;
- diversity and redundancy;
- previous user feedback.

Hard rules such as authorization should remain filters, not soft ranking features.

## Example

Question: “How many unused annual-leave days may carry over?”

Initial vector results:

1. Annual Leave introduction
2. Remote Work approval
3. Carry-over limit: five days
4. Public holiday calendar

A reranker that reads the question with each passage can move the exact carry-over rule to position one.

## Thresholds and Context Budget

After reranking, select passages using score thresholds, a maximum count, and a token budget. Avoid filling unused context with low-quality passages; more context can make generation worse.

Similarity and reranker scores are model-specific, not universal confidence values. Calibrate thresholds on labeled data.

## Failure Modes

- the retriever never returns the correct passage;
- candidates are truncated before the answer-bearing sentence;
- the reranker prefers keyword overlap over true support;
- duplicate chunks occupy every top position;
- an LLM reranker follows instructions hidden in a document;
- latency grows linearly with candidate count.

A reranker cannot recover a candidate that was not retrieved.

## Evaluation

Compare ranking before and after reranking using MRR, nDCG, Precision@k, answer-bearing Recall@k, latency, and final answer quality. Measure whether gains hold across languages, domains, query lengths, and no-answer cases.

## Further Reading

- [ColBERT: Efficient and Effective Passage Search](https://arxiv.org/abs/2004.12832)
- [MonoT5: Text-to-Text Transfer Transformer for Ranking](https://arxiv.org/abs/2003.06713)
