# Multi-Agent Systems

A multi-agent system uses multiple agent instances with different contexts, responsibilities, or tools to pursue a shared goal. Multiple agents do not automatically provide better results; coordination must add more value than it costs.

## Basic Architecture

~~~mermaid
flowchart TD
    U["User goal"] --> O["Orchestrator"]
    O --> R["Research agent"]
    O --> C["Coding agent"]
    O --> E["Evaluation agent"]
    R --> S["Shared artifacts"]
    C --> S
    E --> S
    S --> O
    O --> U
~~~

The agents may use the same underlying model. Their specialization can come from different instructions, tools, context, permissions, or evaluation criteria.

## Coordination Patterns

| Pattern | Structure | Best fit |
|---|---|---|
| Supervisor–workers | One agent delegates and integrates | Variable parallel subtasks |
| Pipeline | Each agent hands off to the next | Stable specialist stages |
| Debate or review | Agents challenge candidate answers | Decisions with clear evidence |
| Blackboard | Agents contribute to shared state | Problems solved incrementally |
| Market or auction | Agents bid for tasks | Large, heterogeneous worker pools |
| Peer collaboration | Agents communicate directly | Research experiments; harder to control |

## When Multiple Agents Help

- subtasks are independent enough to run in parallel;
- different tools, permissions, or expertise should be isolated;
- one agent can evaluate another against an explicit rubric;
- a large search space benefits from diverse exploration;
- the orchestrator can verify and combine outputs.

Avoid multiple agents when one call or a fixed workflow is sufficient, the task is tightly sequential, communication dominates useful work, or no reliable method exists to resolve disagreement.

## Delegation Contract

A good task assignment specifies:

- the concrete objective and expected artifact;
- relevant context and authoritative sources;
- scope boundaries and prohibited actions;
- available tools and permissions;
- completion and quality criteria;
- where results should be written;
- dependencies and reporting format.

Workers should return evidence, assumptions, uncertainties, and blockers—not only a confident conclusion.

## Shared State

Shared state may include task status, artifacts, claims with citations, decisions, and ownership. Use stable identifiers and versioning to prevent two agents from silently overwriting each other.

The orchestrator should remain responsible for the final synthesis. Concatenating worker outputs is not integration: conflicts, duplication, and incompatible assumptions must be resolved.

## Concurrency

Parallelize only work that does not depend on unfinished results. Protect shared resources with ownership rules, transactions, locks, or isolated branches. Define what happens when a worker times out, fails, or returns partial work.

## Failure Modes

- duplicate effort caused by vague assignments;
- cascading hallucinations when agents trust each other without evidence;
- inconsistent state or conflicting edits;
- endless delegation and discussion;
- authority escalation through an over-privileged worker;
- majority voting that repeats the same correlated error;
- lost accountability when no agent owns the final result.

## Safety and Governance

Apply least privilege per agent. A research agent rarely needs write access; an evaluator should not modify the artifact it judges. Require human approval for consequential actions even if several agents agree.

Log delegation, messages, tool calls, artifacts, approvals, and the final synthesis. Sensitive data should be shared only with agents that need it.

## Evaluation

Compare the system with a strong single-agent baseline. Measure task quality, wall-clock time, total tokens and tool calls, coordination overhead, conflict rate, reproducibility, and safety. Multi-agent architecture is justified only when the measured gain outweighs added complexity.

## Related Guides

- [What Is an AI Agent?](what-is-an-agent.md)
- [Planning](planning.md)
- [Agentic Workflows](workflows.md)
- [Coding Agents](coding-agents.md)
