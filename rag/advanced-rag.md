# Advanced RAG

Advanced RAG improves difficult parts of the pipeline after a measured baseline reveals a specific failure. More components are useful only when they produce a verified gain.

## From Naive to Advanced RAG

~~~mermaid
flowchart LR
    Q["Question"] --> RT["Route + transform"]
    RT --> H["Hybrid retrieval"]
    H --> RR["Rerank"]
    RR --> CE["Context expansion"]
    CE --> G["Grounded generation"]
    G --> V["Claim verification"]
    V --> A["Answer or abstain"]
~~~

## Query Rewriting

Convert follow-up questions into standalone queries, expand acronyms, or generate alternative phrasings. Preserve the original query for auditing and search it alongside rewrites when possible.

**HyDE** generates a hypothetical answer and embeds it for retrieval. It may bridge vocabulary gaps, but an incorrect hypothesis can bias the search.

## Hybrid and Multi-Source Retrieval

Combine dense embeddings, lexical search, structured databases, knowledge graphs, and live APIs. Route each sub-question to the source that can answer it most reliably.

For a product-support question, use lexical search for an error code, semantic search for symptoms, and a structured database for warranty status.

## Parent–Child Retrieval

Index small child chunks for accurate matching, then return a larger parent section for generation. This preserves surrounding definitions and exceptions without making every search vector broad.

## Contextual Retrieval

Add document title, heading path, or a short generated context to each chunk before embedding and lexical indexing. Keep added context distinguishable from original text and evaluate the extra indexing cost.

## Multi-Hop RAG

Some questions require evidence from multiple sources:

~~~mermaid
flowchart LR
    Q["Who approves fully remote work?"] --> R1["Retrieve remote-work policy"]
    R1 --> F["Extract: manager approval"]
    F --> R2["Retrieve manager definition"]
    R2 --> A["Compose supported answer"]
~~~

Decompose carefully and retain citations for every hop. Errors can compound across steps.

## Graph RAG

Graph RAG represents entities and relationships explicitly, often adding community summaries for global questions. It can help with relationship-heavy or corpus-wide synthesis but costs more to build, update, and evaluate.

Use a graph only when graph structure matches the problem; do not replace a working search index because the term is fashionable.

## Agentic RAG

An agent can decide which source to search, refine a query, inspect results, and stop when evidence is sufficient. It helps with open-ended research but introduces variable cost, latency, and action risk.

Set step limits, tool permissions, source allowlists, evidence requirements, and explicit stopping conditions.

## Corrective and Self-Reflective RAG

A system may grade retrieved evidence, retry with a different query, or verify generated claims. This can improve difficult cases, but models can confidently approve their own mistakes.

Use independent signals and bounded retries. Never allow an evaluation loop to run indefinitely.

## Multimodal RAG

Documents may contain diagrams, screenshots, charts, audio, or video. Index captions, OCR, layout, and modality-specific embeddings. At generation time, provide the original visual region when exact interpretation matters.

## Caching

Cache embeddings, retrieval results, reranker scores, or completed answers only when keys include document version, model version, prompt version, tenant, permission scope, and relevant time constraints.

Never share a private retrieval cache across authorization boundaries.

## Choosing an Upgrade

| Observed failure | Candidate improvement |
|---|---|
| Synonyms are missed | Dense or multi-query retrieval |
| IDs are missed | Sparse or hybrid retrieval |
| Correct chunk ranks low | Reranker |
| Chunk lacks surrounding rule | Parent–child retrieval |
| Follow-up query is ambiguous | Conversation-aware rewriting |
| Answer needs several sources | Multi-hop retrieval |
| Global corpus question | Graph summaries |
| Unsupported claims | Claim verification and abstention |
| Stale answers | Incremental indexing and version-aware cache |

## Production Checklist

- authoritative sources and ownership are defined;
- ingestion and deletion are observable;
- access control is enforced before generation;
- every component is versioned;
- retrieval and generation have separate evaluations;
- citations resolve to exact evidence;
- prompt injection is tested;
- latency and cost budgets have limits;
- failures degrade safely;
- rollback is available.

## Related Guides

- [Retrieval](retrieval.md)
- [Generation](generation.md)
- [Evaluation](evaluation.md)

## Further Reading

- [HyDE: Precise Zero-Shot Dense Retrieval without Relevance Labels](https://arxiv.org/abs/2212.10496)
- [Self-RAG](https://arxiv.org/abs/2310.11511)
- [Corrective Retrieval-Augmented Generation](https://arxiv.org/abs/2401.15884)
