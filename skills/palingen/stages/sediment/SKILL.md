# Palingen Sediment Stage Skill

## Purpose

Use this stage Skill after the **Understand** stage has produced a sufficiently reliable picture of the existing project's control flow, state flow, side effects, external dependencies, and human intervention points.

The goal of Sediment is to define the new load-bearing structure before detailed code salvage.

Do not decide implementation details prematurely. Establish responsibility boundaries first.

## Required inputs

Read the durable artifacts produced by Understand, especially:

- current project understanding / architecture notes;
- initial Responsibility Map;
- identified workflow-control hotspots;
- state and lifecycle observations;
- human intervention points;
- contract-friction observations;
- important raw evidence or source references.

Keep the root Palingen Skill active while using this stage Skill.

## Core question

For every important responsibility, ask:

> If the Agent is wrong here, what must still remain true?

Everything required to preserve truth, authority, consistency, observability, or recovery is a Harness candidate.

## Load the Harness Mapping reference

Use `skills/palingen/references/harness-mapping.md` as the primary reference for this stage.

Its core rule is:

> Move downward everything that must remain true even if the Agent is wrong: raw evidence, authoritative state, invariants, permissions, lifecycle constraints, and recovery structure.

Do not turn the Harness into a hidden workflow engine.

## Analysis procedure

### 1. Identify authoritative truth

Find existing responsibilities that represent facts rather than interpretations:

- raw tool output;
- requests and responses;
- exit codes;
- generated files;
- timestamps;
- current session/run identifiers;
- executed side effects;
- human approvals or actions.

Mark their future authoritative owner in the Responsibility Map.

### 2. Identify state that must survive interruption

Find state required for:

- pause;
- resume;
- branch;
- retry from a known point;
- reuse of intermediate work;
- audit and replay.

Separate authoritative Fact State from Agent Working State and presentation-only Narrative State.

### 3. Identify true invariants

Extract rules that must remain deterministic even when semantic reasoning changes.

Examples:

- immutable objective or scope;
- evidence integrity;
- valid lifecycle transitions;
- maximum retry or resource limits;
- required approvals;
- transaction or destructive-action boundaries.

Do not mistake current workflow sequencing for an invariant.

### 4. Identify authority and permission boundaries

Distinguish:

- Agent intent;
- Harness authorization;
- Human authority.

Mark risky or irreversible actions that require deterministic policy enforcement and/or explicit human approval.

### 5. Identify lifecycle constraints

Harness may govern execution lifecycle such as:

```text
NEW
RUNNING
WAITING_FOR_HUMAN
PAUSED
COMPLETED
FAILED
```

Harness should not normally dictate semantic business sequencing such as:

```text
A must call B;
B failure must call C;
C success must call D.
```

### 6. Identify recovery structure

Determine which successful intermediate results must remain reusable if a later action fails.

A local failure should not erase prior value.

Mark checkpoint, resume, branch, and artifact-retention requirements.

### 7. Mark what rises rather than sediments

Explicitly mark responsibilities that should remain outside Harness:

- semantic interpretation -> Agent;
- contextual sequencing -> Agent;
- strategy and know-how -> Skill;
- reusable deterministic execution -> Tool candidate;
- deterministic micro-adaptation -> Lubricant candidate.

This negative mapping is required to prevent overgrowth of the Harness.

## Required outputs

Produce or update at least:

### `HARNESS_MAPPING.md`

Map original-project responsibilities to conceptual Harness destinations:

```text
Artifact Store
State Store
Event Store
Policy Engine
Human Approval Gateway
Checkpoint / Recovery
Tool Invocation Boundary
Harness Invariants
```

The implementation does not need to mirror these names as classes or services.

### Responsibility Map update

For each important responsibility, record the proposed ownership shift and the reason.

Examples:

```text
raw CLI stdout
  old owner: workflow code
  new owner: Harness / Artifact Store

interpret authentication failure
  old owner: parser if/else
  new owner: Agent + low-level Skill candidate

production write approval
  old owner: UI confirmation branch
  new owner: Harness policy + Human authority
```

### High-level Skill candidates

Identify high-level knowledge or strategy that belongs to the new structural frame but does not belong in Harness.

## Exit criteria

Do not leave Sediment until the Agent can answer:

1. What facts must remain authoritative even if Agent reasoning is wrong?
2. What state must survive interruption or restart?
3. What rules are true invariants rather than old workflow sequencing?
4. What actions require deterministic permission or Human authority?
5. What successful intermediate work must remain reusable after later failure?
6. What semantic responsibilities have explicitly been kept out of Harness?
7. Which areas remain ambiguous and must be revisited during Disassemble?

The stage is complete when the new load-bearing boundary is clear enough that detailed code disassembly can classify old assets against it.

## Feedback loop

Sediment and Disassemble are allowed to iterate.

If detailed code analysis reveals that a presumed invariant is actually semantic workflow logic, move it back out of Harness. If disassembly discovers hidden authoritative state or permission boundaries, return here and update the Harness Mapping.

A stage boundary is a checkpoint, not a prohibition on revisiting evidence.
