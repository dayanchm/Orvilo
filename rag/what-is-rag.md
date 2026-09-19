# What Is Retrieval-Augmented Generation?

Retrieval-Augmented Generation (**RAG**) is an application architecture that retrieves relevant information from an external source and supplies it to a generative model as evidence for an answer.

The original RAG research combined a parametric language model with non-parametric retrieved memory. In practical systems, the term now covers pipelines that search documents, databases, APIs, or the web before generation.

## The Central Idea

~~~mermaid
flowchart LR
    Q["Question"] --> R["Retriever"]
    K[("Knowledge source")] --> R
    R --> C["Relevant context"]
    Q --> G["Generator"]
    C --> G
    G --> A["Grounded answer"]
~~~

A plain model answers from its training and current prompt. A RAG system first asks: **What evidence should the model see for this question?**

## Simple Example

Knowledge source:

~~~text
Annual Leave Policy
Full-time employees receive 20 days of annual leave.
Unused leave can carry over up to five days.
~~~

Question:

~~~text
How much annual leave does a full-time employee receive?
~~~

Retrieved evidence contains the first policy sentence. The generator can then answer:

~~~text
Full-time employees receive 20 days of annual leave.
Source: Annual Leave Policy
~~~

The model did not need this policy in its training data. It needed the right evidence at answer time.

## Two Phases

| Phase | Runs when | Main operations |
|---|---|---|
| Indexing | Documents are added or changed | Load, clean, chunk, embed, index |
| Querying | A user asks a question | Transform query, retrieve, rerank, generate |

Indexing can run in batches. Querying is latency-sensitive and must enforce the current user's permissions.

## What RAG Can Improve

- **Freshness:** Update the index without retraining the model.
- **Grounding:** Give the model evidence instead of asking it to recall everything.
- **Traceability:** Connect answers to documents and passages.
- **Private knowledge:** Search authorized internal content.
- **Domain coverage:** Supply specialized terminology and facts.
- **Control:** Add, correct, expire, or remove knowledge independently of model weights.

## What RAG Does Not Guarantee

RAG does not automatically make answers correct. Failure can occur when:

1. the right document was never loaded;
2. chunking separated necessary context;
3. retrieval missed the relevant passage;
4. reranking preferred a misleading passage;
5. the prompt did not require evidence;
6. the generator ignored or misread the evidence;
7. citations pointed to a source that did not support the claim.

RAG also does not update the model's underlying knowledge or teach a lasting new behavior.

## RAG Versus Fine-Tuning

Use RAG for changing facts, private documents, citations, and source-controlled answers. Use fine-tuning for repeated behavior, output style, specialized task patterns, or a compact model's performance. Combine them when both knowledge and behavior need improvement.

## Naive and Production RAG

| Naive RAG | Production RAG |
|---|---|
| Fixed-size chunks | Structure-aware chunking |
| One vector query | Hybrid and multi-query retrieval |
| Top-k directly to model | Filtering and reranking |
| No permission model | Document- and chunk-level authorization |
| Answer always generated | Evidence threshold and abstention |
| End-to-end score only | Stage-level evaluation and tracing |

## When RAG Is a Good Fit

Use it when knowledge is too large for every prompt, changes frequently, must remain private, or needs citations. Avoid adding RAG when the answer requires no external knowledge, a deterministic lookup is enough, or no trustworthy knowledge source exists.

## Related Guides

- [Document Loading](document-loading.md)
- [Chunking](chunking.md)
- [Retrieval](retrieval.md)
- [Generation](generation.md)
