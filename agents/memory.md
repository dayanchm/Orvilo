# Memory in AI Agents

Agent memory is information deliberately preserved or retrieved so a system can act consistently beyond a single model call. It is not one database feature and it is not the same as sending the entire conversation every time.

## Memory Architecture

~~~mermaid
flowchart LR
    I["New interaction"] --> W["Working context"]
    W --> D{"Worth retaining?"}
    D -- "No" --> X["Discard"]
    D -- "Yes" --> E["Extract and validate"]
    E --> S[("Memory store")]
    S --> R["Retrieve relevant items"]
    R --> W
~~~

## State, Context, and Memory

| Concept | Lifetime | Example |
|---|---|---|
| Context | One model call | Prompt, tool results, retrieved passages |
| Working state | One task or session | Current plan and completed steps |
| Short-term memory | Recent interactions | A conversation summary |
| Long-term memory | Across sessions | A confirmed user preference |
| External knowledge | Independent source of truth | Documentation or customer database |

A context window is capacity, not memory. Information disappears when it is no longer supplied to the model unless the application stores it elsewhere.

## Common Memory Types

### Episodic Memory

Records events: what happened, when, and with what outcome. It helps an agent resume work or learn from previous attempts.

### Semantic Memory

Stores stable facts and concepts, such as a user's preferred language or an organization's terminology.

### Procedural Memory

Contains reusable instructions, policies, or skills that describe how to perform a task.

### Working Memory

Keeps temporary task information such as a plan, intermediate calculation, or unresolved question.

## Memory Operations

A useful memory system needs more than storage:

1. **Extract:** Identify a candidate fact from an interaction.
2. **Validate:** Check source, scope, consent, and confidence.
3. **Write:** Store it with provenance and timestamps.
4. **Retrieve:** Select only information relevant to the current task.
5. **Reconcile:** Resolve conflicts or prefer a newer authoritative source.
6. **Forget:** Delete expired, incorrect, sensitive, or user-revoked data.

## Retrieval Strategies

| Strategy | Strength | Weakness |
|---|---|---|
| Recent-first | Simple and preserves continuity | Old but important facts disappear |
| Semantic similarity | Finds related meaning | Similar does not always mean relevant |
| Keyword or metadata filter | Precise and auditable | Requires good structure |
| Summary | Saves context space | Can omit nuance or preserve an error |
| Hybrid retrieval | Balances precision and recall | More components to tune |

Retrieval should consider identity, tenant, time, source authority, and task—not vector similarity alone.

## What Should Be Remembered?

Good candidates are durable, useful, explicitly stated facts: preferences, approved decisions, stable project constraints, and confirmed task outcomes.

Avoid retaining secrets, transient emotions, unsupported inferences, unnecessary personal data, or information the user did not expect to persist. Let users inspect, correct, and delete stored memory.

## Failure Modes

- **False memory:** A model-generated inference is stored as fact.
- **Stale memory:** An old preference overrides a newer request.
- **Cross-user leakage:** Tenant or identity filters are missing.
- **Context poisoning:** Malicious content is saved and later treated as instruction.
- **Over-personalization:** The system applies a preference outside its intended scope.
- **Memory overload:** Too many retrieved items distract the model.

Store provenance such as source, creation time, last confirmation, scope, and expiration. Treat memory content as data, not trusted instructions.

## Evaluation

Test whether the agent recalls relevant facts, ignores irrelevant ones, honors corrections and deletion, separates users, resolves contradictions, and performs well when no memory exists. Privacy and deletion tests are as important as retrieval accuracy.

## Related Guides

- [What Is an AI Agent?](what-is-an-agent.md)
- [Tool Use](tool-use.md)
- [Planning](planning.md)
- [Agentic Workflows](workflows.md)
