# Agentification Suitability Assessment

Agentification should not be applied merely because a project is inconvenient, old, or has an awkward UI.

> **Agentification is justified by semantic orchestration, not by software inconvenience alone.**

> **If ordinary refactoring is enough, prefer ordinary refactoring.**

## Gate 0 — Is this actually an Agentification problem?

Before entering the Understand stage, determine whether the target contains a meaningful semantic-orchestration problem.

Ask:

1. Does the project already use an LLM as part of its workflow or decision loop?
2. Does the broader task require interpretation of natural-language, semi-structured, probabilistic, or unstable results?
3. Does a human currently perform semantic orchestration between tools: interpreting outputs, choosing the next tool, resolving ambiguity, or deciding how to recover?

If the answer to all three is effectively **no**, default to recommending conventional software improvement instead of Agentification.

Typical non-Agentification improvements include:

- better installation or dependency scripts;
- simpler defaults and configuration;
- CLI or UI cleanup;
- packaging or containers;
- stable API wrappers;
- ordinary modularization and refactoring;
- deterministic automation.

Do not introduce Agent, Skill, Harness, or LLM-mediated control merely to solve problems that ordinary code can solve cheaply and reliably.

## Strong candidates

### Existing LLM workflow

Projects shaped like:

```text
code
  -> call LLM
  -> parse model output
  -> branch
  -> normalize
  -> retry
  -> call LLM again
```

are strong candidates when large amounts of code exist mainly to pre-encode semantic interpretation and sequencing around the model.

A common transformation is:

```text
Application integrates LLM
        ↓
Agent integrates application capabilities
```

### Human-semantic toolchain

A single deterministic tool without an LLM may not be worth Agentifying, while the larger work environment around it may be.

Example:

```text
scanner
  -> human interprets result
  -> human chooses browser/tool B
  -> human copies data
  -> human judges ambiguity
  -> tool C
```

Here the Agentification target is the **semantic orchestration across tools**, not necessarily the scanner itself.

## Benefit profile

After Gate 0 passes, assess the following qualitatively rather than forcing a false-precision score:

- **Attention Fragmentation** — how much does the user switch between UIs, CLIs, configuration, logs, and tools?
- **Contract Friction** — how much parser, adapter, fallback, lifecycle, and semantic glue exists?
- **Workflow Rigidity** — how often does a fixed sequence conflict with real situations?
- **Semantic Decision Density** — how often must code or humans interpret meaning to decide what happens next?
- **Intermediate Value** — do partial results remain useful when later work fails?
- **Human Judgment Value** — are there probabilistic or contextual decisions where selective human input is valuable?
- **Intervention Friction** — can a human inspect, modify, branch, skip, or resume without restarting the whole workflow?
- **Glue Burden** — how much of the system exists to connect capabilities rather than provide capabilities?

## Cost / counter-signals

Agentification value is reduced when the system is dominated by:

- fixed input and output contracts;
- stable deterministic sequencing;
- low semantic ambiguity;
- hard real-time or very high-throughput constraints;
- highly verifiable algorithmic correctness requirements;
- low glue burden;
- low human or LLM semantic involvement;
- ordinary usability problems that are cheaper to fix directly.

## Recommendation classes

Prefer recommendations such as:

```text
Do not agentify
Light agentification
Partial agentification
Deep agentification
```

`Partial agentification` will often be the most appropriate result.

Do not ask how much of the project can be Agentified. Ask:

> **Where is the highest-leverage Agentification boundary?**

Identify:

- what should remain ordinary software;
- what can remain a coarse Tool;
- where semantic control should move to the Agent;
- where intermediate results should become inspectable;
- where selective human judgment is useful;
- where Harness boundaries are necessary.

## Gate 0 exit outcomes

### NOT_AGENTIFICATION

Use when semantic orchestration is not materially part of the problem.

Recommend ordinary engineering changes and stop the Palingen transformation unless the user explicitly wants further analysis.

### TOOLCHAIN_AGENTIFICATION

Use when individual tools are deterministic but the human currently provides semantic orchestration across them.

Treat the surrounding toolchain/work environment as the transformation target.

### LLM_WORKFLOW_AGENTIFICATION

Use when fixed application code already integrates an LLM and contains substantial parsing, semantic branching, normalization, retries, or model-specific workflow glue.

Proceed to Understand.

### UNCERTAIN

Use when available evidence is insufficient. Perform only enough lightweight inspection to resolve suitability; do not prematurely launch the full transformation.

## Core principle

> **The purpose of suitability assessment is permission to say “do not Agentify this.”**

Palingen should reduce unnecessary work, including unnecessary Agentification.
