# Agentic Workflows

An agentic workflow combines models, tools, and deterministic code into a multi-step system. Workflows keep control flow explicit; agents make dynamic choices where flexibility is valuable.

## Workflow or Agent?

~~~mermaid
flowchart LR
    I["Input"] --> R{"Can the steps be<br/>defined in advance?"}
    R -- "Yes" --> W["Deterministic workflow"]
    R -- "Mostly" --> H["Workflow with<br/>agentic stages"]
    R -- "No" --> A["Agent loop with<br/>strict boundaries"]
~~~

Use the least autonomous design that reliably solves the task. Predictability, latency, debugging, and compliance often matter more than flexibility.

## Core Patterns

### Prompt Chaining

Output from one step becomes input to the next.

~~~mermaid
flowchart LR
    A["Create outline"] --> B{"Validate"}
    B -- "Pass" --> C["Write draft"]
    B -- "Fail" --> A
~~~

Use chaining when a task divides into a stable sequence and intermediate validation improves quality.

### Routing

A classifier sends inputs to specialized paths.

~~~mermaid
flowchart LR
    I["Request"] --> R{"Route"}
    R --> B["Billing"]
    R --> T["Technical support"]
    R --> S["Sales"]
~~~

Use routing when categories are distinct and misrouting can be measured.

### Parallelization

Independent subtasks run concurrently and are aggregated. Sectioning divides the work; voting repeats the same task to obtain diverse judgments. Parallelism reduces wall-clock time but may increase total cost.

### Orchestrator and Workers

An orchestrator decides which subtasks are needed, delegates them, and synthesizes the results. This fits research or coding tasks whose decomposition varies by request.

### Evaluator and Optimizer

A generator creates an artifact; an evaluator checks it against a rubric; the generator revises. Use this only when feedback is specific and improvement is measurable.

### Human Approval

A workflow pauses before consequential actions. The approval screen should show the exact target, proposed change, relevant evidence, and whether the action can be undone.

## Reliability Controls

| Control | Purpose |
|---|---|
| Typed inputs and outputs | Prevent ambiguous handoffs |
| Checkpoints | Persist progress for safe resume |
| Idempotency | Make retries safe |
| Timeouts | Bound slow tools and models |
| Retry policy | Handle transient failures without loops |
| Circuit breaker | Stop repeated calls to a failing dependency |
| Approval gate | Keep humans in control of consequences |
| Compensation | Reverse earlier steps when later work fails |
| Audit trail | Explain what ran, why, and with which data |

## State Machines

Production workflows benefit from explicit states such as queued, running, waiting_for_approval, succeeded, failed, and cancelled. Transitions should be validated in code.

~~~text
queued -> running -> waiting_for_approval -> running -> succeeded
                    \-> cancelled
          \-> failed -> retrying -> running
~~~

Do not encode critical business state only inside a model conversation.

## Data and Control Boundaries

- Keep model-generated content separate from executable commands.
- Validate every handoff against a schema.
- Enforce authentication and authorization outside the model.
- Pass the minimum data required by each stage.
- Treat retrieved text as untrusted input.
- Record model, prompt, tool, and configuration versions.
- Make cancellation and rollback available where practical.

## Observability

A useful trace connects the user request to each model call, tool call, state transition, error, approval, and final artifact. Monitor success rate, latency, token and tool cost, retry count, human escalation, and unsafe-action prevention.

## Testing

Test individual steps, end-to-end paths, and failure recovery. Include malformed model output, empty retrieval, timeout, duplicate delivery, permission denial, partial writes, stale state, cancellation, and evaluator disagreement.

## Related Guides

- [What Is an AI Agent?](what-is-an-agent.md)
- [Planning](planning.md)
- [Tool Use](tool-use.md)
- [Multi-Agent Systems](multi-agent.md)

## Further Reading

- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents)
- [Google ADK workflow agents](https://google.github.io/adk-docs/agents/workflow-agents/)
