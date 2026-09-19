# Instruction Tuning

Instruction tuning teaches a pretrained model to map natural-language requests to useful responses across many tasks. It is usually implemented through supervised fine-tuning on instruction–response demonstrations.

## From Completion to Assistance

A base model sees:

~~~text
Translate English to French:
Good morning ->
~~~

An instruction-tuned model is trained on structured conversations:

~~~text
User: Translate “Good morning” to French.
Assistant: Bonjour.
~~~

Diverse tasks teach the model that the instruction defines the desired transformation.

## Data Structure

~~~mermaid
flowchart LR
    I["Instruction"] --> X["Optional input/context"]
    X --> R["Target response"]
    S["System behavior"] --> R
    R --> F["Formatted chat sequence"]
    F --> L["Assistant-token loss"]
~~~

Examples may include system messages, user turns, assistant responses, tool calls, refusals, and multi-turn corrections.

## Task Diversity

A useful mixture covers question answering, summarization, extraction, transformation, code, reasoning, creative work, tool use, safety, and no-answer cases.

Too much of one format can make the model imitate surface patterns rather than generalize to new instructions.

## Natural and Synthetic Instructions

Human-written examples provide realism and judgment. Synthetic examples scale coverage and difficulty. Generated data should be filtered for correctness, diversity, and leakage from the teacher model.

Templates are efficient but can produce repetitive phrasing that the model overfits.

## Chat Templates

The same messages can be serialized differently by different model families. Training and inference must use compatible role tokens and boundaries.

Loss is commonly masked so the model learns assistant responses without learning to produce the user prompt. Multi-turn choices about which assistant turns receive loss affect behavior.

## Instruction Hierarchy

Training can teach that system instructions outrank user requests and that retrieved documents are data rather than authority. This is not a complete security boundary; application code must still enforce permissions.

Include realistic conflicts and prompt-injection attempts in evaluations.

## Quality Problems

- ambiguous instructions with only one accepted response;
- answers that are fluent but factually unsupported;
- inconsistent refusals;
- accidental personal or confidential data;
- excessive verbosity or repeated disclaimers;
- teacher-model style dominating every response;
- benchmark questions copied into training.

## Evaluation

Use unseen tasks and paraphrases. Measure correctness, instruction following, format compliance, refusal behavior, multi-turn consistency, and capability regression.

Test both underspecified requests that require clarification and answerable requests that should not be refused.

## Related Guides

- [Fine-Tuning](fine-tuning.md)
- [Supervised Fine-Tuning](supervised-fine-tuning.md)
- [Alignment](alignment.md)
