# Evaluating RAG Systems

A RAG system can produce a wrong answer for many different reasons. Evaluation must identify which stage failed rather than assigning one opaque score to the final response.

## Evaluation Layers

~~~mermaid
flowchart TD
    D["Data quality"] --> R["Retrieval quality"]
    R --> C["Context quality"]
    C --> G["Generation quality"]
    G --> S["System quality"]
~~~

| Layer | Key question |
|---|---|
| Ingestion | Was authoritative content parsed and indexed correctly? |
| Retrieval | Did the system find the answer-bearing evidence? |
| Reranking | Did relevant evidence reach the top positions? |
| Generation | Did the answer follow and cite the supplied evidence? |
| End to end | Did the user receive a correct, useful, safe answer? |
| Operations | Was latency, cost, freshness, and availability acceptable? |

## Evaluation Dataset

Each test case can contain:

~~~json
{
  "question": "How many leave days may carry over?",
  "relevant_chunk_ids": ["leave-carryover-01"],
  "reference_answer": "Up to five days.",
  "required_claims": ["maximum is five days"],
  "forbidden_claims": ["all unused days carry over"],
  "answerable": true,
  "user_access_groups": ["employees"]
}
~~~

Build cases from real search logs, subject-matter experts, support questions, and known failures. Remove sensitive data and avoid evaluating only easy questions.

Include paraphrases, exact identifiers, ambiguous questions, multi-hop questions, contradictions, stale documents, multilingual input, access restrictions, and unanswerable requests.

## Retrieval Metrics

- **Recall@k:** fraction of questions whose relevant evidence appears in the first k results.
- **Precision@k:** fraction of retrieved items that are relevant.
- **MRR:** rewards placing the first relevant item near the top.
- **nDCG:** evaluates graded relevance and ordering.
- **Hit rate:** whether at least one relevant item was retrieved.

High Recall@k with poor final answers points toward reranking, context, or generation. Low recall means the answer never had a fair chance.

## Generation Metrics

Evaluate:

- factual correctness;
- faithfulness or groundedness;
- claim-level citation support;
- citation completeness;
- relevance and clarity;
- correct abstention;
- policy and formatting compliance.

String overlap is often insufficient because two correct answers may use different wording.

## Evaluation Modes

| Mode | Strength | Limitation |
|---|---|---|
| Exact rules | Reproducible | Narrow coverage |
| Human review | Nuanced and authoritative | Slow and expensive |
| Model judge | Scalable and flexible | Bias and variability |
| User feedback | Reflects real value | Sparse and confounded |
| Task outcome | Measures actual success | Hard to attribute |

Calibrate model judges against human labels. Preserve the rubric, judge model, prompt, and sampling configuration.

## Oracle Experiments

Use the known correct passage directly with the generator. If the answer remains wrong, retrieval is not the primary problem. Conversely, test retrieval without generation using labeled chunk IDs.

This decomposition prevents teams from tuning embeddings to fix a prompt problem—or changing the generator to hide retrieval failure.

## Online Evaluation

Monitor latency percentiles, error rate, empty retrieval, abstention, citation clicks, user reformulations, escalation, token cost, index freshness, and permission denials. Use guarded A/B tests for major changes.

User thumbs-up is useful but not a complete correctness measure.

## Regression Testing

Pin a test set and run it whenever parsers, chunking, embedding model, index parameters, reranker, prompt, or generator changes. Record component versions so a regression can be reproduced and rolled back.

## Security Tests

Attempt cross-tenant retrieval, prompt injection in documents, malicious files, stale permissions, deleted content, secret extraction, citation spoofing, and tool escalation. A quality improvement never justifies a security regression.

## Further Reading

- [RAGAS: Automated Evaluation of Retrieval-Augmented Generation](https://arxiv.org/abs/2309.15217)
- [BEIR retrieval benchmark](https://arxiv.org/abs/2104.08663)
