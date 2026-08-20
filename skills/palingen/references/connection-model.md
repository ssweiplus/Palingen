# Connection Model Reference

Use this reference when rebuilding how Agent, Tool, Harness, Skill, Human, and retained code connect.

Responsibility Map answers **who owns each responsibility**. Connection Model answers **what kind of connection is required between owners**.

> Use nails for structure, not sequencing.

## Connection types

### Nail

A strong structural constraint required for truth, safety, authority, lifecycle correctness, or recoverability.

Typical examples:

- permission gate;
- mandatory approval;
- immutable objective/scope;
- valid state transition;
- evidence preservation;
- retry/resource ceiling;
- transaction or irreversible-action boundary.

A Nail should remain deterministic and enforceable even if Agent reasoning is wrong.

Do not use Nails to hard-code ordinary semantic sequencing.

### Glue

A semantic/contextual connection whose correct behavior depends on meaning, interpretation, or current context.

Typical examples:

- interpret irregular output;
- choose which capability to invoke next;
- decide whether an error is recoverable;
- correlate heterogeneous results;
- decide whether a retry makes semantic sense.

Glue is usually Agent-mediated, optionally supported by Skill.

### Lubricant

A deterministic helper that reduces representation or transport friction without making semantic decisions.

Typical examples:

- merge SSE chunks;
- strip ANSI sequences;
- convert paths/encodings;
- stable schema adaptation;
- deterministic JSON/text reshaping.

Lubricant should normally remain Code/utility rather than Agent reasoning.

### Remove

Some old connections exist only because the previous workflow architecture required them.

If control inversion makes the connection unnecessary, delete it rather than reimplementing it in a new layer.

## Decision rule

For a connection, ask:

```text
If this connection is wrong, can truth/safety/authority be violated?
  -> Nail

Does correct behavior depend mainly on meaning or context?
  -> Glue

Are the two sides conceptually compatible and only format/transport differs?
  -> Lubricant

Is the connection no longer necessary after responsibility transfer?
  -> Remove
```

## Relationship to Contract Friction

Connection type and friction type are related but not identical.

- Transport/Syntax/Stable Schema friction often becomes Lubricant.
- Semantic/Lifecycle interpretation may become Glue.
- Permission, invariants, and hard lifecycle boundaries become Nails.
- Obsolete workflow-only glue may be Removed.

Do not turn every contract mismatch into Agent Glue.

## Evolution

Connections may change as evidence accumulates:

```text
repeated stable semantic glue -> Lubricant / Code

lubricant becomes safety-critical -> Nail / Harness constraint

stable adapter becomes volatile and semantic -> Agent Glue
```

Promotion or demotion should be evidence-driven, not architectural fashion.

## Connection Map

Create a lightweight `CONNECTION_MAP` only when connection choices are non-obvious or important to explain.

Example:

```yaml
- from: Agent
  to: production-write-tool
  type: Nail
  enforced_by: Harness policy
  reason: irreversible side effect requires authorization

- from: scanner-result
  to: next-tool-selection
  type: Glue
  owner: Agent
  reason: meaning depends on target context

- from: cli-output
  to: artifact-parser
  type: Lubricant
  owner: deterministic utility
  reason: stable formatting difference only
```

## Review questions

1. Are Nails protecting truth/authority rather than dictating workflow?
2. Is semantic Glue visible to the Agent rather than hidden inside Tool code?
3. Is deterministic friction kept as Lubricant instead of wasting model reasoning?
4. Can obsolete old-workflow connections be removed?
5. Did the new design add unnecessary connection layers merely for architectural symmetry?
