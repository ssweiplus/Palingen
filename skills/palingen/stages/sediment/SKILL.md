# Palingen Sediment Stage Skill

## Purpose

Use this stage after Understand has produced a reliable picture of control flow, state flow, side effects, dependencies, artifacts, friction, and human intervention.

The goal is to define the new load-bearing structure before detailed salvage.

Do not decide implementation details prematurely. Establish responsibility boundaries first.

## Required inputs

Read the current:

- project understanding;
- Responsibility Map;
- semantic/workflow-control hotspots;
- contract-friction observations;
- operational artifact observations;
- human-intervention observations.

Keep the root Palingen Skill active.

Load:

- `../../references/harness-mapping.md` as the primary reference;
- `../../references/execution-truth.md` when State/Event/Artifact/recovery semantics are material;
- `../../references/human-role.md` when authority or intervention boundaries are material;
- `../../references/responsibility-allocation.md` when ownership remains ambiguous;
- `../../references/skill-layering.md` when high-level strategy/knowledge candidates are material.

## Core question

> If the Agent is wrong here, what must still remain true?

Everything required to preserve truth, authority, consistency, observability, or recovery is a Harness candidate.

Do not turn the Harness into a hidden workflow engine.

## Analysis

### Authoritative truth and state

Identify execution facts that must remain authoritative and state required for pause, resume, retry, branch, audit, or recovery.

Keep Fact State separate from Agent Working State and Narrative State.

### Invariants and authority

Identify real invariants such as immutable objective/scope, evidence integrity, valid lifecycle transitions, resource/retry limits, and required approvals.

Do not mistake current workflow sequencing for an invariant.

Distinguish:

```text
Agent intent
Harness authorization
Human authority
```

Use the Human Role reference to avoid turning every uncertainty into a blocking approval.

### Artifact compatibility

Identify Operational Artifacts and their real consumers before designing evidence capture.

Record path, format, mutability, lifecycle, and compatibility constraints where material.

Evidence capture may reference, snapshot, copy, hash, or record metadata, but must not break operational use.

### Observability boundary

Identify meaningful execution changes that need to be observable.

Define semantics, not infrastructure. Do not prescribe Event Store, JSONL, tracing, DB audit, or another backend unless the existing project already requires one.

### Recovery structure

Identify which successful intermediate results must remain reusable after later failure and what minimum checkpoint information is needed to continue safely.

### What rises instead

Explicitly keep outside Harness:

- semantic interpretation -> Agent;
- contextual sequencing -> Agent;
- strategy/know-how -> Skill;
- reusable deterministic execution -> Tool/Code candidate;
- deterministic micro-adaptation -> Lubricant candidate.

For high-level Skill candidates, capture strategy, required evidence, decision criteria, heuristics, escalation, and stop conditions. Do not encode end-to-end sequencing. State what the Skill explicitly does not own when that boundary matters.

## Required outputs

Produce/update at least:

### `HARNESS_MAPPING.md`

Record authoritative state, invariants, permission/authority, artifact compatibility, observability semantics, recovery/checkpoint, and tool-invocation boundaries.

Do not require specific storage products or class names.

### Responsibility Map update

Record proposed ownership shifts and rationale.

### Human boundary notes

When material, record which situations are autonomous, reviewable/overrideable, or blocking and which Human role applies.

### High-level Skill candidates

Identify strategy/knowledge that belongs outside Harness. Use a lightweight Skill Map only when multiple Skill boundaries or `does_not_own` constraints would clarify the architecture.

## Exit criteria

Before leaving Sediment, answer:

1. What facts must remain authoritative if Agent reasoning is wrong?
2. What state must survive interruption?
3. What rules are true invariants rather than old sequencing?
4. What actions require deterministic policy or Human authority?
5. Which Operational Artifacts must remain compatible?
6. Which execution changes must be observable without fixing the backend?
7. What successful intermediate work must survive later failure?
8. Which semantic responsibilities are explicitly kept out of Harness?
9. Which high-level knowledge belongs in Skill without owning truth, authority, or sequencing?
10. Which ambiguities must be revisited during Disassemble?

## Feedback loop

Sediment and Disassemble may iterate.

If detailed analysis shows a presumed invariant is semantic workflow logic, move it out of Harness. If hidden authoritative state, artifact contracts, or permission boundaries are discovered, return here and revise the mapping.
