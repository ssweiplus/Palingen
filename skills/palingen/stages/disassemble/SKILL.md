# Palingen Stage Skill — Salvage / Disassemble

## Purpose

Use this stage to dismantle the old project's control structure selectively, salvage reusable capabilities and knowledge, and assign each responsibility to its proposed new owner.

This is not a mandate to maximize decomposition. Prefer the largest safe reuse boundary and split more finely where uncertainty, human judgment, recovery value, or responsibility mixing makes the boundary worth exposing.

## Required inputs

Before entering this stage, load:

- the root `skills/palingen/SKILL.md`;
- current project understanding artifacts;
- current Responsibility Map;
- current Harness Mapping from Sediment;
- `skills/palingen/references/workflow-to-skill.md`;
- `skills/palingen/references/semantic-glue-migration.md`;
- `skills/palingen/references/ephemeral-glue.md` when temporary interface bridging is relevant.

If disassembly reveals that an existing Harness boundary is wrong, revise the Harness Mapping rather than forcing the old assumption to remain true.

## Core analysis

For mixed modules, functions, workflows, and adapters, decompose responsibility into:

```text
Decision
Action
Truth
Knowledge
Permission
```

Then map toward likely destinations:

```text
Decision   -> Agent / deterministic policy / Human
Action     -> Tool / Code
Truth      -> Harness
Knowledge  -> Skill / Reference / Procedure Fragment
Permission -> Harness / Human
```

Also consider:

```text
small deterministic interface friction -> Lubricant
obsolete workflow-only glue            -> Delete
```

## Coarse-first decomposition

Do not split stable implementation solely for architectural purity.

Keep a block coarse when it is:

- deterministic;
- internally mature;
- low in semantic uncertainty;
- not valuable as an independent human intervention point;
- not hiding important truth, authority, or contextual decisions.

Split a boundary more finely when:

- semantic uncertainty is high;
- probability or ambiguity materially affects the next action;
- a human may reasonably want to inspect or override the result;
- partial output has independent value;
- a local failure should not discard successful work;
- permission or safety responsibilities are mixed into execution code.

> **Split where uncertainty becomes valuable.**

## Workflow extraction

Do not translate a fixed workflow into a numbered Skill.

Extract:

- goal;
- required evidence;
- decision criteria;
- heuristics;
- recovery knowledge;
- escalation points;
- stop conditions.

Release unnecessary ordering to Agent composition. Preserve order only where order itself is part of correctness.

Update or create `WORKFLOW_EXTRACTION.md` for meaningful workflows.

## Semantic glue migration

Classify parser/adapter/retry/normalizer logic by friction type and volatility.

Keep deterministic transport and stable structural glue deterministic. Move volatile semantic interpretation upward to the Agent, with low-level Skills where recurring know-how is useful. Preserve raw evidence through the Harness before interpretation.

Update or create `GLUE_MAP.md`.

## Ephemeral Glue

When a temporary low-risk representation mismatch is cheaper to bridge than to formalize, the Agent may generate ephemeral deterministic glue, subject to the project's execution boundary.

Prefer reuse before generation. Record material generated transformations and promote them only when repeated real friction justifies a permanent utility or Tool.

## Knowledge extraction

Extract local recurring know-how into low-level Skills, Procedure Fragments, or References. Do not move mandatory invariants into Skills; send them back to Harness design.

Suggested distinctions:

```text
High-level Skill      -> task strategy and major reasoning structure
Low-level Skill       -> recurring local heuristic or domain know-how
Procedure Fragment    -> local optional operational sequence
Reference             -> factual specification or lookup material
```

## Required outputs

At minimum, update the Responsibility Map and produce enough artifacts to show:

- coarse blocks intentionally retained;
- proposed Tools / Code boundaries;
- low-level Skill / Reference candidates;
- semantic glue moved to the Agent;
- deterministic glue retained as Code or Lubricant;
- old workflow glue proposed for deletion;
- Harness boundary revisions discovered during dismantling;
- human-visible decision points worth exposing.

Use `WORKFLOW_EXTRACTION.md` and `GLUE_MAP.md` when those concerns are materially present. Avoid creating empty process documents merely to satisfy a template.

## Exit criteria

This stage is complete enough to move toward Rebuild when:

- major mixed-responsibility hotspots have proposed destinations;
- reusable deterministic capability boundaries are identifiable;
- important strategy/heuristic knowledge is no longer trapped only in workflow code;
- semantic glue and deterministic glue are distinguishable;
- meaningful human intervention and partial-result boundaries are visible;
- Harness boundary conflicts have been fed back to Sediment artifacts;
- the proposed decomposition is no finer than justified by actual value.
