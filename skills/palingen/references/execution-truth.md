# Execution Truth Reference

Use this reference when State, Event, Artifact, recovery, or observability boundaries are being designed.

## State

Separate three layers:

- **Fact State** — authoritative execution facts owned by Harness or another deterministic source of truth.
- **Working State** — Agent hypotheses, strategy, interpretation, and candidate next actions.
- **Narrative State** — presentation text for humans.

Working or Narrative State must never silently overwrite Fact State.

## Artifact

Distinguish two roles.

### Operational Artifact

A real intermediate or final output used by the original or rebuilt system.

Its path, format, mutability, lifecycle, or consumer behavior may be part of the original contract.

### Evidence Artifact / Reference

A Harness-side copy, snapshot, reference, hash, metadata record, or other evidence used for audit, recovery, replay, or inspection.

> Artifact capture must not break artifact use.

Before changing artifact handling, ask:

- who produces and consumes it?
- is it mutated in place?
- is its path part of the contract?
- is its format externally visible?
- is full copying necessary, or is a reference/hash/metadata enough?

Preserve the original artifact contract unless changing it creates clear and justified value.

## Event / Observability Boundary

Palingen defines meaningful execution-event semantics, not a required storage backend.

Harness-level events may include:

- capability invoked / returned;
- authoritative state changed;
- operational artifact became available;
- human intervention or approval changed;
- checkpoint / branch / resume occurred;
- execution became blocked or recoverable;
- a material failure occurred.

These may be emitted to JSONL, structured logs, OpenTelemetry, a database, ELK/Loki, an internal audit platform, or another observability system.

> Logs describe implementation behavior; Harness events describe execution meaning.

They may share the same backend.

## Failure

A local failure should remain observable with available evidence and partial results.

> Failure is an event with evidence, not necessarily the end of the run.

Do not automatically collapse a failed action into a failed workflow when recovery, branching, replacement, or human intervention remains possible.

## Checkpoint

Checkpoint only what is needed to continue safely:

- required authoritative state;
- relevant artifact references;
- completed side effects;
- necessary permission/approval facts;
- enough lineage to resume or branch.

> Checkpoint what is necessary to continue, not everything that exists.

## Principle

> Preserve compatibility downward; expose observability outward.
