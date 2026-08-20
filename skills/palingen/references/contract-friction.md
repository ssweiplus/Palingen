# Contract Friction Reference

Use this reference during Understand and Disassemble to identify why components require extra adaptation, interpretation, retries, or human bridging.

## Definition

Contract Friction is the cost created when collaborating components disagree or vary in transport, format, structure, lifecycle, semantics, or intent.

It is not automatically a reason to use an Agent.

## Friction layers

### L1 Transport

Examples: HTTP, CLI, SSE, WebSocket, browser interaction, files, stdin/stdout.

Prefer deterministic runtime or adapter handling.

### L2 Syntax / Format

Examples: JSON, YAML, CSV, Markdown, tables, key=value text, ANSI output.

Stable grammar should normally remain deterministic.

### L3 Schema

Examples: field names, layouts, optional values, response envelopes, versioned structures.

Stable formal schemas favor code; unstable or weakly specified structures may require more flexible handling.

### L4 Lifecycle

Examples: login, token expiry, session creation, conversation resume, reconnect, temporary credentials.

Lifecycle facts and limits belong in Harness/deterministic capability; semantic recovery choice may belong to Agent.

### L5 Semantic

Examples: HTTP 200 with business failure, ambiguous tool output, natural-language result interpretation, choosing what evidence means.

This is a primary Agentification target when meaning is contextual or volatile.

### L6 Intent / Social

Examples: human goals, incomplete instructions, Agent-to-Agent handoff, negotiation of constraints or expectations.

Natural-language semantic coordination is usually appropriate here, subject to authority boundaries.

## Friction dimensions

For important friction hotspots, consider:

- **Volatility** — how often the contract changes;
- **Opacity** — how difficult it is to know the real contract;
- **Risk** — consequence of misinterpretation;
- **Frequency** — how often the friction is paid.

Do not build elaborate scoring unless it materially helps a decision.

## Friction Resolution Ladder

Prefer the lowest-cost appropriate treatment:

```text
Remove
  -> Standardize
  -> Encode
  -> Lubricate
  -> Agent-mediate
  -> Human-escalate
```

### Remove

Eliminate obsolete glue or unnecessary coordination created by the old workflow.

### Standardize

Use an existing stable interface or representation when possible.

### Encode

Implement deterministic handling for a stable contract.

### Lubricate

Use small deterministic helpers for representation or transport friction.

### Agent-mediate

Use Agent reasoning when the remaining friction is meaning-dependent, contextual, irregular, or too volatile to justify rigid encoding.

### Human-escalate

Escalate only when authority, irreversible consequence, important ambiguity, or human-only information requires it.

## Intentional friction

Not all friction should be removed.

Approval gates, permission checks, transaction boundaries, destructive-action confirmation, and other safety/authority barriers may be intentional friction.

Preserve or strengthen these in Harness/Human boundaries rather than optimizing them away.

## Key rule

> Agent value is not eliminating all contract friction; it is reducing how much high-variation semantic friction must be pre-encoded.
