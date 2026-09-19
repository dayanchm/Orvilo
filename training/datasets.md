# Training Datasets

A training dataset determines what patterns, languages, domains, and biases a model can learn. Data work includes collection, licensing, filtering, deduplication, mixing, documentation, and evaluation—not simply downloading text.

## Data Pipeline

~~~mermaid
flowchart LR
    S["Sources"] --> C["Collect"]
    C --> P["Parse and normalize"]
    P --> F["Filter"]
    F --> D["Deduplicate"]
    D --> M["Build mixture"]
    M --> V["Validate"]
    V --> SH["Shard and train"]
~~~

## Data Sources

| Source | Potential value | Main concern |
|---|---|---|
| Web pages | Breadth and scale | Quality, consent, duplication |
| Books and articles | Long-form coherence | Copyright and representation |
| Code | Programming and structured reasoning | Licenses, secrets, insecure code |
| Academic material | Technical depth | Narrow style and access rights |
| Conversations | Dialogue behavior | Privacy and consent |
| Human demonstrations | High-quality task behavior | Cost and annotator consistency |
| Synthetic data | Targeted, scalable examples | Teacher errors and reduced diversity |

## Filtering

Filtering can remove spam, malware, personal information, low-quality text, unsafe content, and malformed documents. Classifiers themselves have errors: aggressive filtering can erase dialects, minority languages, or legitimate discussion of sensitive topics.

Record why an item was included or excluded and evaluate filtering across groups and languages.

## Deduplication and Contamination

Exact duplicates overweight repeated documents. Near duplicates include copied articles, templates, mirrored repositories, and lightly edited text.

Deduplication can operate at document, paragraph, or sequence level. It reduces memorization risk and wasted compute, but overly broad matching can remove valid recurring structures.

Evaluation contamination occurs when benchmark questions or solutions appear in training data. Search for exact and approximate overlap before trusting benchmark results.

## Data Mixtures

Datasets compete for a finite token budget. A mixture assigns sampling weights to languages and domains. Sampling proportional to raw volume can underrepresent high-quality or low-resource data; excessive upsampling can cause overfitting.

Track both raw tokens and effective sampled tokens.

## Splits and Versioning

Keep training, validation, and test data separate. Use content hashes, stable source identifiers, collection dates, licenses, filtering versions, and mixture configurations.

A model release should be traceable to an immutable dataset manifest even when raw data cannot be redistributed.

## Governance

Verify collection authority, licenses, privacy obligations, retention, removal requests, regional restrictions, and rules for sensitive data. Security scanning should detect credentials, private keys, malicious payloads, and personal information.

Datasets are not neutral snapshots. Document known gaps and whose language or experience is underrepresented.

## Evaluation

Measure language and domain coverage, quality, toxicity, personal-data rate, duplicates, benchmark overlap, token distribution, source concentration, and downstream model behavior.

Manual review of stratified samples remains important because aggregate classifiers can hide systematic failures.

## Related Guides

- [Tokenization](tokenization.md)
- [Pretraining](pretraining.md)
- [Synthetic Data](synthetic-data.md)
