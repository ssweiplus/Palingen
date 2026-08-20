# Semantic Glue Migration

Use this reference to decide what to do with parsers, adapters, normalizers, retry branches, fallbacks, and cross-component glue found in an existing project.

The goal is not to remove all glue. The goal is to place each kind of friction in the layer best suited to absorb it.

## Glue categories

### Transport glue
Examples: SSE framing, WebSocket transport, stdout/stderr capture, encoding conversion, HTTP mechanics.

Typical owner: deterministic Code / Lubricant.

### Stable structural glue
Examples: stable field renames, DTO mapping, fixed schema conversion, CSV to JSON.

Typical owner: deterministic Code / Adapter / Lubricant.

### Semantic glue
Examples: interpreting irregular CLI output, deciding whether HTTP 200 means business success, diagnosing an ambiguous failure, choosing retry versus strategy change.

Typical owner: Agent, often supported by low-level Skill.

### Workflow glue
Examples: A fails -> B, B fails -> C, C has no result -> mutate input -> retry A.

If the branching depends on context or meaning, release the sequence to the Agent rather than preserving it as fixed orchestration.

## Four diagnostic questions

For each glue segment ask:

1. Is it handling transport/representation, or interpreting meaning?
2. Can the rule be described by a stable grammar or formal contract?
3. How volatile is the contract it depends on?
4. What happens if the interpretation is wrong?

## Default placement

```text
Stable transport friction       -> Lubricant / Code
Stable schema friction          -> Code / Adapter
Volatile semantic friction      -> Agent
Recurring domain know-how       -> Skill
Truth / permission boundary     -> Harness
Old workflow-only compatibility -> Delete
```

## Guardrails

> **Do not replace deterministic adapters with LLM interpretation just because you can.**

> **Do not fossilize volatile semantics into code just because you can parse it today.**

> **Preserve raw evidence before interpretation or normalization.**

Avoid universal response schemas that force irregular systems into a false shared semantic contract. Normalize only structures that are demonstrably stable and repeatedly useful.

## Evidence-driven movement

Ownership may change with real usage.

```text
Agent semantic glue
   -> repeated and stable
Low-level Skill / deterministic pattern
   -> sufficiently stable and valuable
Adapter / Lubricant / Tool
```

Conversely, a deterministic parser that accumulates brittle fallbacks and semantic special cases is a candidate to move upward toward Agent interpretation.

## Suggested artifact

Create or update `GLUE_MAP.md`:

```yaml
- source: src/client.py:80-140
  purpose: interpret CLI authentication failures
  current_form: regex + if/else
  friction_type: semantic
  volatility: high
  proposed_action: move interpretation to Agent
  retain:
    - raw output capture
    - exit code parsing
  support_skill:
    - cli-auth-recovery
```
