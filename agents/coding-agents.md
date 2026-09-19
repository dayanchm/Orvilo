# Coding Agents

A coding agent is an AI agent that can inspect a software project, plan changes, edit files, run development tools, and verify the result. Its value comes from closing the loop between generated code and evidence from the real repository.

## Development Loop

~~~mermaid
flowchart LR
    U["Task"] --> I["Inspect repository"]
    I --> P["Plan change"]
    P --> E["Edit"]
    E --> T["Test and analyze"]
    T --> V{"Verified?"}
    V -- "No" --> D["Diagnose"]
    D --> E
    V -- "Yes" --> R["Report result"]
~~~

## Typical Capabilities

| Capability | Examples |
|---|---|
| Repository exploration | Search symbols, read configuration, inspect history |
| Editing | Add features, fix bugs, update tests and documentation |
| Execution | Run tests, linters, builds, type checks, and formatters |
| Diagnosis | Interpret failures, logs, stack traces, and diffs |
| Coordination | Use issue trackers, CI results, or review feedback |
| Verification | Confirm behavior and summarize remaining risks |

A coding agent should first learn the repository's structure, conventions, and local instructions. Existing code and tests are evidence about intended behavior.

## A Safe Working Method

1. Clarify the desired behavior and boundaries.
2. Inspect relevant files, tests, and configuration.
3. Check the working tree and preserve unrelated user changes.
4. Make the smallest coherent change.
5. Run focused tests, then broader checks when risk warrants them.
6. Review the diff for accidental edits and exposed secrets.
7. Report what changed, what passed, and what remains uncertain.

## Tool Design for Coding

Useful tools expose file reading, precise search, patch-based editing, language servers, tests, builds, version control, and sandboxed execution. Tool output should preserve exit status and avoid truncating the most relevant error.

Prefer structured edits or patches over rewriting entire files. Restrict destructive commands, broad filesystem access, credential access, and outbound network actions.

## Context Management

Repositories are larger than model context windows. Retrieve only relevant files, keep a map of important symbols, and summarize discoveries with file paths. Re-read source before editing if earlier context may be stale.

Generated summaries are navigation aids, not authoritative source code.

## Verification Pyramid

~~~mermaid
flowchart TD
    A["Static checks<br/>format, lint, types"] --> B["Focused tests"]
    B --> C["Integration tests"]
    C --> D["Build or end-to-end checks"]
    D --> E["Human review / deployment evidence"]
~~~

Not every change requires every layer. Match verification effort to blast radius: documentation needs link and formatting checks; authentication or data migrations need deeper tests and review.

## Common Failure Modes

- changing code before understanding the architecture;
- inventing APIs or dependencies that are not installed;
- overwriting unrelated work in a dirty tree;
- fixing symptoms without reproducing the defect;
- weakening tests to make them pass;
- claiming success without running relevant checks;
- executing generated code with excessive permissions;
- expanding scope beyond the user's request.

## Security

Repository content, issues, dependencies, and tool output can contain malicious instructions. Treat them as data. Never expose secrets to the model unnecessarily, use isolated execution, constrain network access, and require approval for publishing, deployment, or destructive changes.

## Evaluation

Use real repository tasks with deterministic checks where possible. Measure patch correctness, regression rate, test quality, unnecessary changes, tool efficiency, security compliance, and the accuracy of the final report.

## Related Guides

- [What Is an AI Agent?](what-is-an-agent.md)
- [Planning](planning.md)
- [Tool Use](tool-use.md)
- [Agentic Workflows](workflows.md)
