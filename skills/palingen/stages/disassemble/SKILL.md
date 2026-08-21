# Palingen Stage Skill — Salvage / Disassemble

## Purpose

Use this stage to dismantle the old control structure selectively, salvage reusable capabilities and knowledge, and assign each responsibility to its proposed new owner.

This is not a mandate to maximize decomposition.

> Prefer the largest safe reuse boundary and split where uncertainty becomes valuable.

## Required inputs

Keep the root Skill active and use the current project understanding, Responsibility Map, and material Harness/authority decisions established so far.

Use a separate Harness Mapping only when one actually exists and remains useful; it is not a required input.

Load when relevant:

- `../../references/responsibility-allocation.md`
- `../../references/contract-friction.md`
- `../../references/workflow-to-skill.md`
- `../../references/skill-layering.md`
- `../../references/semantic-glue-migration.md`
- `../../references/ephemeral-glue.md`
- `../../references/human-role.md`
- `../../references/connection-model.md` when connection type matters;
- `../../references/domain-semantic-seeding.md` only when semantic seeding was explicitly enabled by the user for this run.

If detailed analysis reveals a wrong Harness boundary, revise Sediment rather than forcing the assumption.

## Responsibility decomposition

For mixed modules/functions/workflows/adapters, separate:

```text
Decision
Action
Truth
Knowledge
Permission
```

Then map toward likely owners:

```text
Decision   -> Agent / deterministic policy / Human
Action     -> Tool / Code
Truth      -> Harness
Knowledge  -> Skill / Reference / Procedure Fragment
Permission -> Harness / Human
```

Use the six dimensions from `responsibility-allocation.md` when the owner is unclear:

```text
Determinism
Semantic Dependency
Contract Volatility
Truth Criticality
Risk / Authority
Composability
```

Also consider Lubricant for small deterministic interface friction and Delete for obsolete workflow-only glue.

## Coarse-first decomposition

Keep a block coarse when it is deterministic, mature, low in semantic uncertainty, not hiding important truth/authority/contextual decisions, and not valuable as an independent intervention point.

Split more finely when:

- semantic uncertainty is high;
- ambiguity materially affects the next action;
- a human may reasonably inspect or override the result;
- partial output has independent value;
- a local failure should not discard successful work;
- permission/safety responsibilities are mixed into execution;
- the boundary is needed to transfer semantic control to the Agent.

Do not create micro-Tools or micro-Skills for architectural purity.

## Workflow and Skill extraction

Do not translate fixed workflow sequencing into a numbered Skill.

Extract goal, required evidence, decision criteria, heuristics, recovery knowledge, escalation points, and stop conditions.

Classify reusable knowledge as High-level Skill, Low-level Skill, Procedure Fragment, or Reference using `skill-layering.md`.

For meaningful Skill candidates, state what they teach and what they explicitly do **not** own. Mandatory truth, permission, evidence, and lifecycle constraints stay outside Skill.

Release unnecessary ordering to Agent composition. Preserve order only when order is part of correctness.

Use `WORKFLOW_EXTRACTION.md` and/or a lightweight Skill Map only when materially useful.

## Contract and semantic glue analysis

For parser/adapter/retry/normalizer code, first ask what kind of friction it solves.

Prefer the Friction Resolution Ladder:

```text
Remove -> Standardize -> Encode -> Lubricate -> Agent-mediate -> Human-escalate
```

Keep stable transport/schema handling deterministic. Move volatile semantic interpretation upward to the Agent, supported by Skill when recurring knowledge is useful.

Preserve raw evidence before interpretation.

Use `GLUE_MAP.md` only when materially useful.

## Domain semantic refinement

Only when semantic seeding was explicitly enabled, refine what detailed code analysis can clarify.

Distinguish:

- implementation names from durable business concepts;
- local aliases from genuinely different concepts;
- business rules from workflow mechanics;
- business state from execution/runtime state;
- business relationships from accidental code coupling.

Preserve provenance and uncertainty. Use candidate mappings rather than forced equivalence when another project or vocabulary appears similar.

Do not require OWL, SHACL, a reasoner, or a canonical shared vocabulary in Palingen v1.

The semantic seed remains a sidecar for future cross-project alignment, not an authoritative control model.

If semantic seeding was not enabled, do not start it opportunistically during this stage.

## Connection candidates

When important owner-to-owner boundaries are non-obvious, classify the connection:

```text
Nail       -> truth / safety / authority / hard lifecycle structure
Glue       -> semantic or contextual composition
Lubricant  -> deterministic representation/transport adaptation
Remove     -> obsolete connection from the old workflow
```

Do not use a Nail to recreate ordinary workflow sequencing, and do not use Agent Glue for stable deterministic friction.

A `CONNECTION_MAP` is optional; create it only when it materially clarifies Rebuild.

## Ephemeral Glue

Temporary low-risk representation mismatches may be bridged with generated deterministic glue through the project's constrained execution boundary.

Prefer existing Tool/utility/simple deterministic transformation before generating new code. Record material generated transformations and promote them only when repeated real friction justifies permanence.

## Human decision points

Do not mark every uncertain branch as a Human checkpoint.

Classify meaningful intervention as autonomous, reviewable/overrideable, or blocking. Blocking should be reserved for authority, irreversibility, important evidence deficiency, or human-only information/capability.

## Information to carry forward

At minimum, update the Responsibility Map and preserve enough accepted information to show:

- coarse blocks intentionally retained;
- proposed Tool/Code boundaries;
- semantic decisions moved toward Agent control;
- Skill/Reference candidates and important `does_not_own` boundaries;
- deterministic vs semantic glue treatment;
- important Nail/Glue/Lubricant/Remove connection candidates when relevant;
- old workflow glue proposed for deletion;
- Harness revisions;
- Operational Artifact compatibility constraints discovered in code;
- human-visible decision/intervention points worth exposing;
- candidate Agentification Slices for Rebuild.

An updated Domain Semantic Seed is optional and only relevant when semantic seeding was enabled.

Avoid empty process documents.

## Exit criteria

Move toward Rebuild when:

- major mixed-responsibility hotspots have proposed owners;
- reusable deterministic capability boundaries are identifiable;
- important knowledge is no longer trapped only in workflow code;
- Skill candidates do not own truth, authority, or hidden global sequencing;
- semantic and deterministic glue are distinguishable;
- important structural vs semantic connections are distinguishable where needed;
- meaningful artifact/recovery/human boundaries are visible;
- candidate slices can transfer control without unnecessary decomposition;
- Harness conflicts have been fed back to Sediment;
- decomposition is no finer than justified by actual value.

Domain ontology completeness is never an exit requirement for v1.
