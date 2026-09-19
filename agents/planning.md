# Planning in AI Agents

Planning is the process of turning a goal into actions while accounting for constraints, dependencies, evidence, and uncertainty. An agent may plan everything at the start, choose only the next action, or combine both approaches.

## Planning Cycle

~~~mermaid
flowchart TD
    G["Goal + constraints"] --> P["Propose plan"]
    P --> A["Choose next action"]
    A --> O["Observe real result"]
    O --> C{"Plan still valid?"}
    C -- "Yes" --> D{"Done?"}
    C -- "No" --> P
    D -- "No" --> A
    D -- "Yes" --> V["Verify outcome"]
~~~

## Planning Strategies

| Strategy | How it works | Best fit |
|---|---|---|
| Fixed workflow | Code defines every step | Stable, regulated processes |
| Plan then execute | Create a full plan before acting | Predictable multi-step tasks |
| Receding horizon | Plan a few steps, then reconsider | Changing environments |
| Next-action reasoning | Choose one action from current evidence | Search and diagnosis |
| Search over alternatives | Compare multiple candidate paths | Small spaces with clear scoring |
| Planner–executor | Separate planning from tool execution | Complex tasks needing oversight |

Long plans can become stale after the first unexpected result. Replanning should respond to evidence, not merely rewrite the plan repeatedly.

## What Makes a Good Plan?

A good plan:

- states the desired outcome and completion test;
- respects user constraints and permissions;
- orders prerequisites before dependent actions;
- distinguishes assumptions from verified facts;
- identifies risky or irreversible steps;
- includes checkpoints and fallback paths;
- is detailed enough to guide action but easy to revise.

## Dependencies and Parallel Work

~~~mermaid
flowchart LR
    A["Collect requirements"] --> B["Design"]
    B --> C["Implement API"]
    B --> D["Implement UI"]
    C --> E["Integration test"]
    D --> E
    E --> F["Release review"]
~~~

Tasks C and D can run in parallel only after B is complete. A dependency graph prevents premature actions and helps expose the true critical path.

## Planning With Tools

The agent should plan around actual tool contracts and permissions. It must not assume that a tool exists, a write succeeded, or data is current. Each action produces an observation that may confirm, invalidate, or refine the plan.

Before a consequential action, include:

1. the exact target;
2. the expected change;
3. required authorization;
4. validation or preview;
5. recovery or rollback;
6. success evidence.

## Progress Tracking

Track concrete state rather than vague confidence:

| Field | Example |
|---|---|
| Goal | “Publish the reviewed release notes” |
| Completed | Drafted and fact-checked |
| Current | Waiting for owner approval |
| Remaining | Publish and verify URL |
| Blocker | Approval not received |
| Evidence | Review record and preview link |

A task is not complete merely because all planned steps were attempted. Completion requires evidence that the intended result exists.

## Common Failure Modes

- planning before understanding the goal;
- over-planning a simple task;
- treating a guess as a dependency;
- continuing after the environment changes;
- retrying the same failed action without new information;
- marking success without verification;
- hiding blockers instead of asking for human judgment;
- optimizing for activity rather than outcome.

## Evaluation

Planning quality should be measured by task success, unnecessary steps, recovery from surprises, constraint compliance, cost, and the correctness of stopping decisions. Test with missing tools, conflicting requirements, partial failures, and changed external state.

## Related Guides

- [What Is an AI Agent?](what-is-an-agent.md)
- [Tool Use](tool-use.md)
- [Memory](memory.md)
- [Agentic Workflows](workflows.md)
