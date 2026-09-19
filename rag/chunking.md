# Chunking

Chunking divides a document into retrieval units. Each chunk should be small enough to match a focused query but large enough to preserve the evidence needed for an answer.

## Why Chunk?

Embedding an entire handbook produces one broad representation. A query about annual leave may not strongly match it. Splitting by meaningful sections makes the relevant policy easier to retrieve.

~~~mermaid
flowchart TD
    D["Employee Handbook"] --> R["Remote Work section"]
    D --> L["Annual Leave section"]
    D --> E["Expenses section"]
    L --> C1["Entitlement: 20 days"]
    L --> C2["Carry-over: 5 days"]
~~~

## Common Strategies

| Strategy | Method | Strength | Risk |
|---|---|---|---|
| Fixed tokens | Split every N tokens | Fast and predictable | Breaks structure |
| Recursive | Try paragraph, sentence, then token boundaries | Practical default | Still size-driven |
| Structure-aware | Split by headings, sections, rows, or functions | Preserves meaning | Format-specific |
| Semantic | Split when topic similarity changes | Topic coherence | More cost and tuning |
| Parent–child | Retrieve small chunks, return larger parent | Precise search plus context | More index logic |
| Late chunking | Encode long context before deriving chunk vectors | Retains surrounding meaning | Model/runtime constraints |

## Chunk Size Tradeoff

Small chunks improve precision but can lose definitions, exceptions, and references. Large chunks preserve context but increase cost and may dilute the matching signal.

There is no universal best size. Start from document structure, then tune using retrieval evaluation. Token counts matter more than character counts because embedding and generation limits are token-based.

## Overlap

Overlap repeats boundary text in neighboring chunks. It can protect facts split across fixed windows, but excessive overlap creates duplicates, increases storage, and crowds retrieval results.

Prefer natural structural boundaries first. Use overlap as a measured correction, not a default substitute for good parsing.

## Contextualizing a Chunk

A raw chunk may say:

~~~text
It may be carried over for one year.
~~~

Add document and section context:

~~~text
Document: Employee Handbook
Section: Annual Leave
Unused annual leave of up to five days may be carried over for one year.
~~~

Context improves retrieval and makes isolated passages interpretable. Do not add invented summaries as if they were source text; label generated context separately.

## Metadata Per Chunk

Store chunk ID, parent document ID, version, heading path, page or offsets, source URI, timestamps, language, access groups, and checksum. Keep exact character or token offsets when citations need highlighting.

## Code, Tables, and Conversations

- Split code around modules, classes, and functions; preserve signatures and imports.
- Repeat table headers with rows or serialize rows into self-contained statements.
- Group conversations by topic or turn window while preserving speaker names.
- Keep legal clauses with their definitions and exceptions when possible.

## Testing Chunking

Create question–evidence pairs and check whether at least one chunk contains enough information to answer. Track answer-bearing chunk recall, duplication, token distribution, orphan headings, and chunks exceeding model limits.

Visually inspect random samples. Statistics alone will not reveal broken reading order or missing table semantics.

## Related Guides

- [Document Loading](document-loading.md)
- [Embeddings](embeddings.md)
- [Retrieval](retrieval.md)
