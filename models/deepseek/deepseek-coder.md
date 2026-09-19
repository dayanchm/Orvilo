# DeepSeek Coder

## A Language-Model Family for Programming

**DeepSeek Coder**, released in 2023, is a family of decoder-only language models trained primarily for code generation, completion, and understanding.

Models were released at several sizes, from roughly **1B to 33B parameters**, in both Base and Instruct forms.

## Training Data

Each model was trained from scratch on **2 trillion tokens**:

```text
87% source code
13% English and Chinese natural language
```

The code corpus included project-level data rather than only isolated functions. This helps a model learn relationships between files, imports, classes, tests, and documentation.

## Code Completion and Infilling

Normal generation predicts what comes after a prefix:

```text
def add(a, b): → return a + b
```

DeepSeek Coder was also trained for **fill-in-the-middle (FIM)** tasks:

```text
Code before the gap + code after the gap → missing code
```

FIM is useful in editors because the missing section often sits between existing code. The models support a context window of up to **16K tokens**, allowing more project context to be included.

## Base vs. Instruct

- **Base** models are suited to completion, research, and further fine-tuning.
- **Instruct** models are adapted to respond to requests such as “write a test” or “explain this function.”

## What It Can Be Used For

- Generating functions and tests
- Completing or infilling code
- Explaining and translating code
- Finding likely bugs
- Answering programming questions

Generated code must still be reviewed and tested. A syntactically valid answer can contain security flaws, incorrect assumptions, or nonexistent APIs.

## Why It Mattered

DeepSeek Coder established a dedicated code-model line and supplied the coding expertise later combined with general chat capabilities in DeepSeek-V2.5.

## Source

- [Official DeepSeek Coder repository](https://github.com/deepseek-ai/DeepSeek-Coder)
