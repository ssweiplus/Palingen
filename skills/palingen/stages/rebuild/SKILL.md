# Palingen Rebuild Stage Skill

## Purpose

Rebuild the minimum architecture needed to transfer the intended responsibilities without destroying working deterministic capability.

Rebuild is not a clean-room rewrite and not an architecture-purity exercise.

> Migrate responsibility, not files.

> Architectural purity is not the goal; responsibility correction is.

## Required inputs

Keep the root Palingen Skill active and use the current:

- project understanding and Gate 0 rationale;
- Responsibility Map;
- Harness Mapping;
- workflow/glue extraction artifacts when present;
- Skill Map and Connection Map when present;
- identified Tool, Skill, Human, and retained-code boundaries;
- candidate Agentification Slices from Disassemble.

Load these references when relevant:

- `../../references/target-form.md`
- `../../references/execution-truth.md`
- `../../references/human-role.md`
- `../../references/responsibility-allocation.md`
- `../../references/skill-layering.md`
- `../../references/connection-model.md`

## Minimal rebuild

Ask first:

> What is the smallest change that transfers the intended control ownership and produces meaningful Agentification value?

Prefer to keep mature deterministic modules, API clients, storage formats, CLI behavior, and operational artifacts unless changing them creates clear value.

Do not rewrite stable code merely to make the new architecture look uniform.

## Side-by-side reconstruction

Prefer a working old path beside the emerging Agentified path when practical.

Do not destroy a trusted execution path before the replacement has earned trust.

Use the old implementation as a behavioral and compatibility reference during migration.

## Agentification Slice

Use a small but complete control slice as the default migration unit.

A slice usually contains:

```text
Input
  -> capability/action
  -> decision boundary
  -> state/artifact/evidence
```

For each selected slice, leave a lightweight Slice Plan or equivalent record containing:

- retained/exposed capability;
- semantic decision transferred to Agent;
- Skill/Reference knowledge used, including important `does_not_own` boundaries;
- Harness truth/invariant/permission/recovery constraints;
- Human role/intervention mode where relevant;
- Operational Artifact compatibility constraints;
- important connection types (Nail / Glue / Lubricant / Remove) when they affect implementation;
- expected local validation evidence.

Prefer this over a large migration roadmap.

## Transfer control ownership

Measure progress by control ownership rather than file movement.

Example:

```text
old:
A -> semantic parser -> branch -> B

new:
A -> raw/evidenced result
          |
        Agent
          |
          B
```

The implementation is incomplete if the old workflow still secretly makes the semantic decision before the Agent sees the evidence.

## Connection design

Use `connection-model.md` when the relationship between owners matters.

Apply:

```text
Nail      -> deterministic structural constraint
Glue      -> semantic/contextual composition
Lubricant -> deterministic interface-friction reduction
Remove    -> obsolete old-workflow connection
```

Use Nails for truth, safety, authority, and hard lifecycle structure—not to hard-code ordinary sequencing.

Keep stable transport/format adaptation deterministic rather than spending Agent reasoning on it.

## Preserve execution truth

Rebuild must preserve the distinction between:

- authoritative Fact State;
- Agent Working State;
- presentation-only Narrative State.

Do not let Agent interpretation overwrite execution truth.

Operational artifacts remain usable by the original or retained code. Evidence capture may reference, snapshot, copy, or hash them, but must not silently change their path, format, mutability, or lifecycle contract.

Emit meaningful execution changes through an observability boundary without requiring a specific logging or event-storage backend.

## Human interaction

Expose human intervention where authority, irreversibility, meaningful ambiguity, or human-only information makes it valuable.

Do not convert uncertainty into approval spam.

Prefer:

```text
autonomous
reviewable / overrideable
blocking only when necessary
```

Ask humans at the level of intent and consequence rather than implementation detail.

## Skill integrity

Skills should provide strategy/heuristics while the Agent retains contextual composition.

Do not let implementation pressure turn a Skill into a numbered hidden workflow, or move mandatory truth/authority constraints into prose because it is convenient.

## Composition review

Before declaring a slice rebuilt, check:

1. Does the underlying capability still work?
2. Did the intended semantic decision really move to the Agent?
3. Are authoritative truth and permissions still deterministic?
4. Are Operational Artifacts still compatible and usable?
5. Can meaningful intermediate work survive local failure?
6. Is human intervention available at the intended granularity without becoming mandatory everywhere?
7. Did a Tool, Skill, Harness, Nail, or adapter accidentally recreate the old workflow?
8. Is deterministic friction still deterministic rather than Agent-mediated without reason?
9. Does the Slice Plan contain enough evidence for later Slice Validation?

## Exit criteria

Rebuild is ready for Validate when selected slices are runnable, their Slice Plans/evidence exist where useful, and the intended responsibility transfer can be observed in practice.

Do not wait for every possible module to be transformed. Preserve intentionally coarse regions and record deferred boundaries only when useful.
