# Tool Use in AI Agents

Tools let an agent retrieve facts, run computations, change external systems, and verify whether an action succeeded. The model decides **what** to request; application code remains responsible for validating and executing it.

## Tool-Use Loop

~~~mermaid
sequenceDiagram
    participant U as User
    participant A as Agent
    participant V as Validator
    participant T as Tool
    U->>A: Goal
    A->>V: Structured tool request
    V->>V: Check schema and permission
    V->>T: Execute approved request
    T-->>A: Observation
    A->>U: Result or next question
~~~

A tool call should be a typed request, not arbitrary prose. The runtime validates its name and arguments, executes it, and returns a result that the model can observe.

## Anatomy of a Tool

| Element | Purpose |
|---|---|
| Name | Distinguishes the operation from other tools |
| Description | Explains when the model should use it |
| Input schema | Defines valid argument names and types |
| Output contract | Makes success and failure interpretable |
| Permissions | Limits which resources and actions are allowed |
| Side-effect level | Marks the call as read-only, reversible, or destructive |
| Timeout and retries | Bounds execution and transient failure handling |

~~~json
{
  "name": "get_order",
  "description": "Read one order by its public order ID.",
  "input": {
    "type": "object",
    "properties": {
      "order_id": { "type": "string" }
    },
    "required": ["order_id"],
    "additionalProperties": false
  }
}
~~~

## Read and Write Tools

Read-only tools search, inspect, or calculate. Write tools send messages, create records, spend money, modify permissions, or delete data.

Use stricter controls as consequences increase:

| Action | Recommended control |
|---|---|
| Read public documentation | Automatic execution |
| Read private business data | Authentication and audit log |
| Create a reversible draft | Preview and undo |
| Send, purchase, publish, or delete | Explicit approval and idempotency |
| Change credentials or permissions | Strong authentication and separate authorization |

## Designing Good Tools

- Give one tool one clear responsibility.
- Use unambiguous names and descriptions.
- Prefer constrained fields and enums over free-form strings.
- Return compact structured data plus actionable error details.
- Include stable identifiers, not only display names.
- Separate preview from commit for consequential actions.
- Make repeated requests safe with idempotency keys.
- Paginate large results instead of flooding the model context.

A small set of distinct tools is generally easier for a model to select correctly than many overlapping operations.

## Errors Are Observations

Tools should distinguish invalid input, missing data, denied permission, temporary failure, and permanent failure. The agent can correct an argument or choose another path only when the error is explicit.

Do not silently convert a failed write into apparent success. Return machine-readable status and a human-readable explanation.

## Tool Security

Tool results and retrieved documents are **untrusted input**. They may contain prompt injection that asks the model to ignore its instructions or expose secrets.

Defenses include:

- keep system instructions separate from tool output;
- never place secrets in model-visible context unless essential;
- enforce permissions in code, not in prompts;
- validate destinations, file paths, URLs, and database queries;
- sandbox code execution and restrict network access;
- require approval based on the action, not the model's confidence;
- log the request, authorization decision, result, and actor.

## Testing Tool Use

Evaluate tool selection, argument accuracy, permission handling, error recovery, unnecessary calls, and final-answer grounding. Include unavailable tools, malformed output, timeouts, duplicate requests, misleading retrieved text, and partial success.

## Related Guides

- [What Is an AI Agent?](what-is-an-agent.md)
- [Planning](planning.md)
- [Memory](memory.md)
- [Agentic Workflows](workflows.md)

## Further Reading

- [Model Context Protocol specification](https://modelcontextprotocol.io/specification/)
- [Google ADK tools documentation](https://google.github.io/adk-docs/tools/)
- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents)
