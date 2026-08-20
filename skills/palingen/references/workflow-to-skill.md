# Workflow to Skill Conversion

Use this reference when dismantling a rigid workflow. The goal is not to rewrite the workflow as prose. The goal is to preserve strategy and correctness while releasing unnecessary sequencing.

> **Extract the strategy; release the sequence.**

Preserve mandatory order only when the order itself is part of correctness.

## Conversion questions

For each workflow, ask:

1. What outcome is the workflow really trying to achieve?
2. Which steps are implementation means rather than goals?
3. Which branches are semantic or contextual decisions?
4. Which recurring heuristics or recovery lessons are worth retaining?
5. Which ordering constraints are truly mandatory?
6. Which intermediate results are valuable enough to preserve, expose, branch from, or hand to a human?

## Reallocation model

```text
Goal / strategy / heuristics   -> Skill
Contextual decisions           -> Agent
Deterministic actions          -> Tool / Code
Mandatory invariants/order     -> Harness
High-risk authority            -> Human
Obsolete workflow-only glue    -> Delete
```

## Coarse-first rule

Prefer the largest safe unit of reuse. Do not split stable deterministic internals merely because they can be split.

> **Prefer the largest safe unit of reuse.**

Split more finely where uncertainty becomes valuable:

- semantic uncertainty is high;
- risk or authority matters;
- a human decision is valuable;
- intermediate results have independent value;
- recovery from a partial failure matters.

> **Stable regions stay coarse; uncertain regions expand into inspectable decision points.**

## Skill anti-pattern

Bad conversion:

```text
Step 1: call A
Step 2: call B
Step 3: if B fails call C
Step 4: retry A
```

This is still a workflow, only expressed in prose.

Better extraction:

```text
Goal
Required evidence
Decision criteria
Heuristics
Recovery knowledge
Escalation points
Stop conditions
```

A Skill should constrain reasoning without unnecessarily owning sequencing.

## Human visibility

Do not turn every uncertain point into a blocking approval. Prefer three levels:

```text
Agent may continue automatically
Human can inspect / override
Human confirmation is required
```

> **Expose uncertainty without forcing attention.**

## Suggested artifact

Create or update `WORKFLOW_EXTRACTION.md` with entries such as:

```yaml
workflow: retry_auth_flow
goal: restore usable authenticated execution

keep_as_block:
  - token refresh HTTP exchange

extract_to_skill:
  - distinguish token, session, permission, and service failures
  - preserve reusable context
  - avoid repeated identical retries

move_to_agent:
  - choose recovery strategy
  - decide whether to resume or recreate the session

move_to_harness:
  - retry ceiling
  - credential state
  - audit trail

human:
  - provide new credentials when required

delete:
  - brittle string-based semantic retry switch
```
