# Contributing to Orvilo

Thank you for helping improve Orvilo. The project is a learning-oriented collection of clear, multilingual resources about artificial intelligence and language-model history.

## Ways to Contribute

You can help by:

- Correcting technical or historical inaccuracies
- Improving explanations, diagrams, and examples
- Adding a missing model or model generation
- Fixing grammar, links, or formatting
- Translating existing material without removing the original content

## Before You Start

1. Search existing issues and pull requests to avoid duplicate work.
2. For a large new section or structural change, open a documentation issue first.
3. Use primary sources whenever possible: official technical reports, model cards, papers, and vendor documentation.
4. Do not copy substantial passages from a source. Explain the material in your own words and link to the source.

## Repository Structure

```text
Orvilo/
├── README.md
├── assets/                 Images used by the documentation
└── models/
    ├── transformer.md      Individual concepts
    ├── deepseek/           DeepSeek model family
    ├── gemini/             Gemini model family
    ├── gpt/                GPT model family
    ├── llama/              Llama model family
    ├── mistral/            Mistral model family
    └── qwen/               Qwen model family
```

## Documentation Style

- Write in clear, direct English unless a document is explicitly multilingual.
- Introduce an acronym before using it repeatedly.
- Explain why a technique matters, not only what it is called.
- Distinguish model families, checkpoints, API aliases, and product names.
- Do not invent parameter counts, training data, benchmark results, or release dates.
- State when a vendor has not publicly disclosed a technical detail.
- Include limitations; fluent output is not proof of factual correctness.
- Prefer short diagrams, tables, and examples when they make a relationship easier to understand.

## File and Link Conventions

- Use lowercase kebab-case Markdown filenames, such as `neural-language-model.md`.
- Model version dots are allowed, such as `gpt-4.1.md`.
- Use `README.md` for directory indexes.
- Use relative links for files inside the repository.
- Store reusable images in `assets/` and provide meaningful alternative text.
- Check that every new relative link resolves from the document containing it.

## Adding a Model Family

A model-family directory should normally contain:

1. One Markdown file for each major generation represented in the repository.
2. A `README.md` with a recommended reading order.
3. A Mermaid evolution diagram with relative links.
4. A factual comparison table.
5. A capability matrix whose legend explains its symbols.
6. Links to primary or official sources.

Avoid treating benchmark scores from different evaluation settings as directly comparable.

## Local Checks

Before opening a pull request, run:

```bash
git diff --check
```

The command should report no whitespace errors. Also confirm that every documentation file added or modified by your change contains meaningful content.

Also review changed Markdown in a renderer that supports GitHub-flavored Markdown and Mermaid diagrams.

## Commits and Pull Requests

Use a concise Conventional Commit-style title:

```text
docs: add Llama model comparison
fix(gemini): correct context-window information
```

Supported title types are `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `build`, `ci`, `chore`, `perf`, and `revert`.

In the pull request description:

- Explain what changed and why.
- Identify the files or model families affected.
- Link related issues and primary sources.
- List the checks you performed.
- Mention any factual uncertainty or follow-up work.

By contributing, you agree that your work may be distributed under the repository's license.
