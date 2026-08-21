# Palingen Sediment Stage Skill

## Purpose

Define the new load-bearing responsibility boundary before detailed salvage.

Do not decide implementation details prematurely. Establish what must remain correct and authoritative even when Agent reasoning is wrong.

## Required inputs

Use the current project understanding, Responsibility Map, semantic/workflow-control hotspots, operational artifact observations, and human-intervention observations.

Keep the root Palingen Skill active.

Load when relevant:

- `../../references/harness-mapping.md`
- `../../references/execution-truth.md`
- `../../references/human-role.md`
- `../../references/responsibility-allocation.md`
- `../../references/skill-layering.md`

## Core question

> If the Agent is wrong here, what must still remain true?

Truth, authority, consistency, evidence, and recovery requirements are Harness candidates.

Do not turn the Harness into a hidden workflow engine.

## Analysis

### Authoritative truth and state

Identify facts that must remain authoritative and state required for safe continuation or recovery.

Keep Fact State separate from Agent Working State and Narrative State.

### Invariants and authority

Identify real invariants such as immutable objective/scope, evidence integrity, resource/retry ceilings, hard lifecycle/transaction constraints, and required approvals.

Do not mistake current workflow sequencing for an invariant.

Distinguish:

```text
Agent intent
Harness authorization
Human authority
```

### Artifact compatibility

Identify Operational Artifacts and their real consumers before designing evidence capture.

Preserve path, format, mutability, lifecycle, and compatibility when material.

Evidence capture may reference, snapshot, copy, hash, or record metadata, but must not break operational use.

### Observability and recovery

Identify meaningful execution changes that should remain observable and the minimum accepted state/evidence needed to continue after interruption.

Define semantics, not infrastructure. Do not prescribe Event Store, JSONL, tracing, database audit, or another backend unless the target independently requires one.

### What stays outside Harness

```text
semantic interpretation -> Agent
contextual sequencing    -> Agent
strategy / know-how      -> Skill
reusable execution       -> Tool / Code
small deterministic friction -> Lubricant / Code
```

For high-level Skill candidates, capture useful strategy and `does_not_own` boundaries without encoding an end-to-end workflow.

## Information to carry forward

Update the Responsibility Map with material Harness/authority decisions, including where relevant:

- authoritative state/facts;
- invariants and permissions;
- artifact compatibility constraints;
- evidence/observability semantics;
- recovery/checkpoint requirements;
- human authority/intervention boundaries;
- semantic responsibilities explicitly excluded from Harness.

A separate Harness Mapping is **optional**. Create one only when the Harness boundary is complex enough that a dedicated view materially improves later reasoning or review.

Likewise, Human-role notes or Skill maps are conditional views rather than mandatory files.

## Exit criteria

Move toward Disassemble when the Agent can answer:

1. What must remain authoritative if Agent reasoning is wrong?
2. What must survive interruption?
3. Which rules are true invariants rather than old sequencing?
4. What requires deterministic policy or Human authority?
5. Which Operational Artifacts must remain compatible?
6. Which execution changes need durable observability semantics?
7. Which semantic responsibilities are explicitly kept out of Harness?
8. Which ambiguities should be revisited during Disassemble?

## Feedback loop

Sediment and Disassemble may iterate.

If detailed analysis shows a presumed invariant is semantic workflow logic, move it out of Harness. If hidden truth, artifact, recovery, or permission boundaries appear later, revise the smallest relevant part of this boundary.
