# Document Loading

Document loading converts source material into clean, structured records that later stages can chunk, index, retrieve, and cite. Poor ingestion cannot be repaired by a better language model.

## Ingestion Flow

~~~mermaid
flowchart LR
    S["Source"] --> F["Fetch"]
    F --> P["Parse"]
    P --> N["Normalize"]
    N --> M["Add metadata"]
    M --> V["Validate"]
    V --> O["Versioned documents"]
~~~

## Common Sources

| Source | Parsing concern |
|---|---|
| Markdown or text | Headers, code blocks, encoding |
| HTML | Navigation, ads, hidden content, canonical URL |
| PDF | Reading order, columns, tables, OCR |
| Office documents | Headings, comments, sheets, formulas |
| Database | Stable IDs, joins, permissions, timestamps |
| API | Pagination, rate limits, deleted records |
| Audio or video | Transcription, speakers, timestamps |
| Scanned image | OCR confidence and layout |

A PDF is a visual layout format, not a reliable sequence of paragraphs. Always inspect extraction quality on representative documents.

## Document Record

~~~json
{
  "document_id": "handbook-2026",
  "version": "2026-09-01",
  "title": "Employee Handbook",
  "source_uri": "docs://hr/handbook.pdf",
  "section": "Annual Leave",
  "language": "en",
  "effective_at": "2026-09-01",
  "access_groups": ["employees"],
  "checksum": "…",
  "text": "Full-time employees receive 20 days…"
}
~~~

Stable IDs make updates and deletion possible. Provenance fields make citations and audits possible. Access metadata must travel with the content.

## Cleaning Without Destroying Meaning

Remove repeated headers, footers, menus, and broken whitespace. Preserve headings, lists, table relationships, code boundaries, page numbers, and meaningful punctuation.

Do not silently rewrite facts during cleaning. Keep the original artifact or a content hash so parsed output can be audited.

## Tables and Images

A flattened table can lose the relationship between headers and cells. Convert each row into self-contained text, preserve the structured representation, or use a model that can interpret the original layout.

For diagrams and images, store captions, nearby text, OCR, alt text, and page coordinates. A multimodal retrieval path may be preferable when visual structure is essential.

## Updates and Deletion

Use incremental indexing:

1. detect new, changed, and deleted documents;
2. parse only affected sources;
3. create a new document version;
4. rebuild affected chunks and embeddings;
5. atomically switch the searchable version;
6. remove expired vectors and cached results.

A deleted source must disappear from the search index, caches, and derived stores.

## Security

Fetch content only from approved locations. Defend against malicious files, oversized payloads, parser vulnerabilities, and server-side request forgery. Scan uploads and isolate parsers.

Document text is untrusted. Phrases such as “ignore previous instructions” are content, not commands. Label sources clearly when passing them to a model.

## Quality Checks

Measure parse success, missing text, duplicated boilerplate, OCR confidence, language detection, metadata completeness, permission coverage, and time from source update to searchable index.

Create golden documents with known headings, tables, lists, and expected extracted text to catch parser regressions.

## Related Guides

- [What Is RAG?](what-is-rag.md)
- [Chunking](chunking.md)
- [Embeddings](embeddings.md)
