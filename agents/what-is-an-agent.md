# What Is an AI Agent?

An **AI agent** is a system that uses a model to decide how to pursue a goal, take actions through tools, inspect the results, and adapt its next step. Unlike a basic chatbot, an agent can interact with an environment instead of only producing text.

The model is the reasoning component, but the complete agent also includes instructions, tools, state, permissions, and a control loop.

## The Agent Loop

~~~mermaid
flowchart LR
    G["Goal"] --> P["Plan or choose<br/>the next action"]
    P --> A["Act through<br/>a tool"]
    A --> O["Observe<br/>the result"]
    O --> E{"Goal reached?"}
    E -- "No" --> P
    E -- "Yes" --> R["Return result"]
    E -- "Blocked or risky" --> H["Ask a human"]
~~~

A typical execution follows five stages:

1. **Understand:** Interpret the user's goal, constraints, and available context.
2. **Plan:** Select the next useful action or divide the goal into smaller tasks.
3. **Act:** Call a tool, query a data source, run code, or communicate with another system.
4. **Observe:** Read the real result instead of assuming the action succeeded.
5. **Adjust:** Continue, recover from an error, ask for help, or stop.

The loop needs an explicit stopping condition, such as successful completion, a maximum number of steps, a budget limit, or a request for human approval.

## Core Components

| Component | Purpose | Example |
|---|---|---|
| Model | Interprets the task and selects actions | A language or multimodal model |
| Instructions | Define the role, rules, and desired behavior | “Never send an email without approval” |
| Tools | Let the agent affect or inspect its environment | Search, database, calendar, terminal |
| State | Holds information needed during the current run | Tool results, task progress, intermediate output |
| Memory | Preserves selected information across runs | User preferences or prior decisions |
| Retrieval | Supplies relevant external knowledge | Product documentation or company policies |
| Guardrails | Restrict inputs, outputs, and actions | Access control, validation, approval gates |
| Evaluator | Measures whether the result is acceptable | Tests, schemas, rubrics, or human review |

Memory and state are related but not identical. **State** is the working context of a task; **memory** is information deliberately retained for future tasks.

## Agent, Chatbot, and Workflow

| System | Who controls the steps? | Can use tools? | Best suited to |
|---|---|:---:|---|
| Chatbot | User and a single model response | Sometimes | Questions, drafting, and conversation |
| Workflow | Predefined application code | Yes | Predictable, repeatable processes |
| Agent | The model dynamically chooses actions | Yes | Open-ended tasks with uncertain steps |

A workflow might always run classify → retrieve → summarize. An agent can decide whether retrieval is needed, choose a source, inspect the result, and change its approach.

Agentic behavior is a spectrum. A system may use fixed workflow stages but allow an agent to make decisions inside one stage. More autonomy is not automatically better: deterministic code is usually preferable when the correct sequence is already known.

## Common Agent Patterns

### Tool-Using Agent

One model chooses among tools and repeats the action-observation loop. This is the simplest useful agent architecture.

### Router

A model classifies the request and sends it to a specialized prompt, model, tool, or agent. Routing is useful when task categories are distinct.

### Planner and Executor

A planner proposes steps while an executor carries them out. The plan may be revised when observations contradict its assumptions.

### Evaluator and Optimizer

One component produces a result and another evaluates it against explicit criteria. The system iterates only when the feedback is actionable.

### Orchestrator and Workers

An orchestrator dynamically creates or delegates subtasks, then combines the workers' results. This pattern fits tasks whose decomposition cannot be known in advance.

### Human-in-the-Loop Agent

The agent pauses before consequential, ambiguous, or irreversible actions. Human review is especially important for payments, external messages, deletion, access changes, and high-stakes decisions.

## A Minimal Example

~~~text
messages = [user_goal]

repeat until step_limit:
    decision = model(messages, available_tools)

    if decision is a final answer:
        return decision

    if decision requires approval:
        ask the user before continuing

    observation = execute_validated_tool_call(decision)
    messages += [decision, observation]

return "Stopped because the step limit was reached."
~~~

The important detail is that tool results return to the model as observations. Without this feedback, the model cannot reliably know whether its action worked.

## When an Agent Is a Good Fit

Use an agent when:

- the goal is clear but the necessary steps depend on intermediate results;
- the system must search, inspect, compare, or recover from errors;
- tools provide verifiable feedback from the environment;
- the task benefits enough to justify additional latency and cost;
- actions can be safely constrained and monitored.

Prefer a direct model call or fixed workflow when:

- one response is enough;
- the steps are stable and can be encoded deterministically;
- errors would be difficult to detect or reverse;
- the environment provides no reliable feedback;
- strict latency, cost, or compliance requirements outweigh flexibility.

## Safety and Reliability

Agents amplify both model capability and model error because they can act on their outputs.

| Risk | Practical mitigation |
|---|---|
| Hallucinated facts | Ground responses in trusted data and require citations |
| Incorrect tool calls | Validate arguments with schemas and business rules |
| Prompt injection | Treat tool output and retrieved content as untrusted data |
| Excessive permissions | Use least-privilege credentials and scoped tools |
| Destructive actions | Add previews, approval gates, backups, and rollback |
| Infinite loops | Set step, time, token, and cost limits |
| Hidden failure | Log decisions, tool calls, observations, and final status |
| Data leakage | Minimize retained data and isolate users and sessions |

Tool descriptions are part of the agent's interface. They should clearly state what an operation does, when it should be used, its parameters, and its side effects.

## Evaluating an Agent

Do not evaluate only the final prose. Measure the complete trajectory:

- **Task success:** Did the system actually achieve the goal?
- **Correctness:** Are claims and generated artifacts valid?
- **Tool selection:** Did it choose the right tools and arguments?
- **Efficiency:** How many model calls, tool calls, tokens, and seconds were used?
- **Recovery:** Can it detect a failed action and choose a better approach?
- **Safety:** Did it respect permissions and approval requirements?
- **Trace quality:** Can a reviewer understand what happened?

Build evaluations from representative tasks, known edge cases, adversarial tool output, permission failures, and realistic long-running scenarios.

## Key Principle

An agent is not simply “an LLM with tools.” It is a controlled system in which a model can choose actions, learn from real observations, and continue until a well-defined stopping condition is met.

Start with the simplest architecture that solves the problem. Add memory, planning, multiple agents, or greater autonomy only when evaluation shows that the added complexity improves the result.

## Continue Learning

~~~mermaid
flowchart LR
    A["Agent basics"] --> T["Tool use"]
    T --> P["Planning"]
    P --> M["Memory"]
    M --> W["Workflows"]
    W --> C["Coding agents"]
    W --> X["Multi-agent systems"]

    click T "tool-use.md"
    click P "planning.md"
    click M "memory.md"
    click W "workflows.md"
    click C "coding-agents.md"
    click X "multi-agent.md"
~~~

| Guide | Main question |
|---|---|
| [Tool Use](tool-use.md) | How can an agent safely act in an environment? |
| [Planning](planning.md) | How does an agent choose and revise its steps? |
| [Memory](memory.md) | What should an agent retain and retrieve? |
| [Agentic Workflows](workflows.md) | How should multi-step systems be structured? |
| [Coding Agents](coding-agents.md) | How can agents change and verify software? |
| [Multi-Agent Systems](multi-agent.md) | When does delegation among agents help? |

## Further Reading

- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents)
- [Google Agent Development Kit documentation](https://google.github.io/adk-docs/)
- [Model Context Protocol specification](https://modelcontextprotocol.io/specification/)
