# Retrieval-Augmented Generation

Retrieval-Augmented Generation (**RAG**) gives a language model relevant external evidence before it answers. Instead of relying only on information encoded during training, the application searches a controlled knowledge source and asks the model to produce a response grounded in the retrieved passages.

## Complete Pipeline

~~~mermaid
flowchart LR
    subgraph Indexing["Offline indexing"]
        D["Documents"] --> L["Load and clean"]
        L --> C["Chunk"]
        C --> E["Embed"]
        E --> V[("Search index")]
    end

    subgraph Query["Online query"]
        Q["Question"] --> QR["Rewrite or expand"]
        QR --> S["Retrieve"]
        V --> S
        S --> RR["Rerank"]
        RR --> P["Build grounded prompt"]
        P --> G["Generate answer"]
        G --> A["Answer + citations"]
    end

    A --> EV["Evaluate and monitor"]
~~~

## Learning Path

~~~mermaid
flowchart LR
    W["1. RAG basics"] --> D["2. Document loading"] --> C["3. Chunking"]
    C --> E["4. Embeddings"] --> V["5. Vector search"]
    V --> R["6. Retrieval"] --> RR["7. Reranking"]
    RR --> G["8. Generation"] --> EV["9. Evaluation"]
    EV --> A["10. Advanced RAG"]

    click W "what-is-rag.md"
    click D "document-loading.md"
    click C "chunking.md"
    click E "embeddings.md"
    click V "vector-search.md"
    click R "retrieval.md"
    click RR "reranking.md"
    click G "generation.md"
    click EV "evaluation.md"
    click A "advanced-rag.md"
~~~

| Step | Guide | Main question |
|---:|---|---|
| 1 | [What Is RAG?](what-is-rag.md) | Why retrieve information before generation? |
| 2 | [Document Loading](document-loading.md) | How does raw content become trustworthy text? |
| 3 | [Chunking](chunking.md) | How should documents be divided? |
| 4 | [Embeddings](embeddings.md) | How is semantic meaning represented numerically? |
| 5 | [Vector Search](vector-search.md) | How are similar vectors found efficiently? |
| 6 | [Retrieval](retrieval.md) | How do we find complete and relevant evidence? |
| 7 | [Reranking](reranking.md) | How do we improve the initial ranking? |
| 8 | [Generation](generation.md) | How does the model answer from evidence? |
| 9 | [Evaluation](evaluation.md) | How do we measure each stage separately? |
| 10 | [Advanced RAG](advanced-rag.md) | How do production systems handle difficult queries? |

## Running Example

The guides use a fictional employee handbook:

~~~text
Remote Work Policy
Employees may work remotely up to three days per week.
Manager approval is required for a fully remote arrangement.

Annual Leave Policy
Full-time employees receive 20 days of annual leave.
Unused leave can carry over up to five days.
~~~

For the question **“How many annual-leave days can a full-time employee receive?”**, the system should retrieve the Annual Leave Policy, ignore the semantically nearby Remote Work Policy, answer **20 days**, and cite the source.

## RAG Compared with Other Approaches

| Approach | Updates knowledge by | Strength | Limitation |
|---|---|---|---|
| Prompt context | Supplying text manually | Simple and immediate | Does not scale |
| RAG | Retrieving external evidence | Fresh, traceable, controllable | Retrieval can fail |
| Fine-tuning | Changing model weights | Teaches style or behavior | Poor fit for frequently changing facts |
| Web search agent | Searching live sources | Current and broad | Less predictable source quality |
| Long-context model | Supplying large documents | Preserves global context | Higher cost and distraction risk |

RAG and fine-tuning solve different problems and can be combined: fine-tune behavior, retrieve knowledge.

## Production Principles

- Preserve provenance from the original document to every chunk.
- Enforce access control before retrieval results reach the model.
- Evaluate retrieval separately from generation.
- Prefer abstention over an unsupported confident answer.
- Treat documents as untrusted data that may contain prompt injection.
- Log versions of documents, embedding models, indexes, prompts, and generators.
- Design citations so users can inspect the actual supporting passage.

## Further Reading

- [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401)
- [Dense Passage Retrieval](https://arxiv.org/abs/2004.04906)
- [Sentence-BERT](https://arxiv.org/abs/1908.10084)
