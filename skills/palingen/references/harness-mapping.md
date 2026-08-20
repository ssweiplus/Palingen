# Harness Mapping Reference

Use this reference during the **Sediment** stage to identify which responsibilities from an existing project should move downward into the Harness.

Load `execution-truth.md` when State, Artifact, Event/Observability, checkpoint, or recovery behavior is being mapped.

The central rule is:

> Move downward everything that must remain true even if the Agent is wrong: raw evidence, authoritative state, invariants, permissions, lifecycle constraints, and recovery structure.

Harness does not own the business workflow. It owns the conditions under which any workflow remains truthful, authorized, observable, and recoverable.

## Conceptual Harness responsibilities

```text
Harness
├── Authoritative State
├── Evidence / Artifact References
├── Event / Observability Boundary
├── Policy / Permission Boundary
├── Human Authority Boundary
├── Checkpoint / Recovery
├── Tool Invocation Boundary
└── Invariants
```

These are conceptual responsibilities, not required classes, services, storage engines, or filenames.

## Existing-project responsibility mapping

| Existing responsibility | Typical destination | Why it sediments |
| --- | --- | --- |
| authoritative session/run/action facts | Authoritative State | must survive Agent error and interruption |
| raw response/stdout/stderr/material evidence | Evidence capture/reference | interpretation must remain traceable |
| meaningful execution changes | Event / Observability Boundary | execution meaning must remain observable |
| immutable objective/scope/limits | Invariants | Agent drift must not rewrite task truth |
| permission/dangerous-operation checks | Policy / Permission Boundary | authority must not depend on probabilistic reasoning |
| required human authorization | Human Authority Boundary | human authority must be explicit |
| pause/resume/branch/recovery facts | Checkpoint / Recovery | local failure must not erase prior value |
| tool call parameters/side effects/results | Tool Invocation Boundary | execution truth needs a deterministic mediation point |

## State model

Distinguish:

### Fact State — authoritative

Examples:

- session identifier actually returned;
- tool exit code;
- artifact/reference identifier;
- current execution lifecycle state;
- approval actually granted;
- action already executed.

### Working State — Agent hypothesis

Examples:

- likely root cause;
- strategy;
- interpretation;
- candidate next action.

### Narrative State — presentation

Human-readable summaries and explanations.

Working or Narrative State must not silently overwrite Fact State.

## Artifact compatibility

Do not assume every original output should be moved into an Artifact Store.

Distinguish:

- **Operational Artifact** — the real file/object/output used by the old or rebuilt system;
- **Evidence Artifact / Reference** — copy, snapshot, reference, hash, metadata, or other capture used for audit/recovery.

Operational artifact path, format, mutability, and lifecycle may be part of the original contract.

> Artifact capture must not break artifact use.

Preserve the original operational contract unless changing it creates clear value.

## Event / Observability

Do not prescribe an Event Store.

Harness defines which execution changes are meaningful to expose, while the implementation may use:

```text
structured logging
JSONL
OpenTelemetry / tracing
DB audit records
ELK / Loki
existing internal observability
another suitable backend
```

> Logs describe implementation behavior; Harness events describe execution meaning.

Possible Harness-level events include capability invocation/result, authoritative state change, artifact availability, human intervention, approval change, checkpoint/branch/resume, blocked state, and material failure.

## Decision types

```text
Semantic Decision
  what does this mean?
  what should we try next?
        -> Agent

Mechanical Decision
  retry_count >= limit
  invalid state transition
  missing required evidence
        -> Harness

Authority Decision
  production write
  destructive action
  scope expansion
        -> Harness policy and/or Human
```

## What should NOT sediment

Keep outside Harness:

- contextual semantic interpretation;
- dynamic business strategy;
- dynamic choice of next capability;
- product-specific know-how;
- fixed end-to-end business workflow;
- volatile semantic parsers that are not stable contracts.

Prefer Agent, Skill, Tool, Code, or Lubricant according to the responsibility.

## Required Sediment artifact

Produce `HARNESS_MAPPING.md` or an equivalent project artifact that records:

- source responsibility/code evidence;
- proposed Harness responsibility;
- why it must remain authoritative/deterministic;
- operational artifact compatibility constraints;
- Event/Observability semantics when material;
- Human authority involved;
- unresolved boundary ambiguity.

Do not force a specific physical storage architecture.

## Exit questions

Before leaving Sediment, answer:

1. Which facts must remain authoritative if Agent reasoning is wrong?
2. Which state must survive pause, failure, restart, or branch?
3. Which checks are true invariants/authority boundaries rather than workflow sequencing?
4. Which operational artifacts must remain compatible and usable?
5. Which execution changes must be observable without prescribing the backend?
6. Which human interventions represent true authority?
7. Which semantic decisions must remain outside Harness?

If these are unclear, the Harness boundary is not stable enough to proceed.
