# Palingen Rebuild Stage Skill

## Purpose

Rebuild the minimum architecture needed to transfer the intended responsibilities without destroying working deterministic capability.

Rebuild is not a clean-room rewrite and not an architecture-purity exercise.

> Migrate responsibility, not files.

## Inputs

Keep the root Palingen Skill active and use the current:

- Gate 0 / project boundary;
- Responsibility Map;
- material Harness/authority decisions;
- workflow/glue/Skill/Connection views when they actually exist;
- identified Tool, Skill, Human, retained-code boundaries;
- candidate Agentification Slices from Disassemble.

Load references only when relevant:

- `../../references/target-form.md`
- `../../references/execution-truth.md`
- `../../references/human-role.md`
- `../../references/responsibility-allocation.md`
- `../../references/skill-layering.md`
- `../../references/connection-model.md`

## Minimal rebuild

Ask first:

> What is the smallest change that transfers the intended control ownership and produces meaningful Agentification value?

Prefer to keep mature deterministic modules, API clients, storage formats, CLI behavior, and Operational Artifacts unless changing them creates clear value.

Use side-by-side reconstruction where practical; do not destroy a trusted execution path before the replacement has earned trust.

## Agentification Slice

Use a small but complete control slice as the default migration unit.

A slice often contains:

```text
retained/exposed deterministic capability
+ semantic decision boundary
+ truth / artifact / authority boundary
```

Do **not** require a separate Slice Plan for every slice.

Before implementation, make sure the following are known somewhere durable when they materially affect later work:

- capability being retained or exposed;
- semantic decision being transferred;
- relevant Skill/Reference knowledge and important `does_not_own` boundaries;
- Harness truth/invariant/permission/recovery constraints;
- Human intervention mode where relevant;
- Operational Artifact compatibility constraints;
- important Nail / Glue / Lubricant / Remove choices;
- evidence expected to prove the transfer worked.

Use the Responsibility Map, run-state whiteboard, issue/notes, implementation patch, or a lightweight Slice Plan—whichever creates the least unnecessary artifact overhead.

## Transfer control ownership

Measure progress by control ownership rather than file movement.

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

The transfer is incomplete if the old workflow still secretly makes the semantic decision before the Agent sees the evidence.

## Preserve boundaries

### Execution truth

Fact State remains authoritative. Agent Working State and Narrative State must not silently overwrite it.

Operational Artifacts remain usable by their real consumers. Evidence capture may reference, snapshot, copy, hash, or record metadata without silently changing artifact contracts.

### Connections and workflows

Use Nails only for hard truth, safety, authority, and lifecycle structure. Keep stable transport/format friction deterministic. Let semantic/contextual composition remain visible to the Agent.

A deterministic workflow may remain inside a Tool or retained code when its ordering is genuinely part of correctness or the capability itself. Do not dismantle it merely because it is a workflow.

Conversely, do not preserve accidental sequencing that still owns contextual semantic decisions better left to the Agent.

### Human interaction

Prefer autonomous + reviewable behavior. Block only when authority, irreversibility, important evidence deficiency, or human-only capability makes it necessary.

The rebuilt user surface should use domain language by default. Do not require end users to understand Palingen stages, Tool identifiers, Harness states, Slice terminology, retry policies, or internal acceptance enums merely to operate the product.

A chat-shaped interface is not automatically Agentic. If the conversation repeatedly asks the user to choose internal tools, approve routine steps, or advance workflow states, the old mechanical orchestration may simply have moved into the chat UI.

### Skill integrity

Skills provide strategy and know-how. Do not let implementation pressure turn them into numbered global workflows or move mandatory truth/authority constraints into prose.

## Composition review

Before considering a meaningful slice ready for Validate, check:

1. Does the underlying capability still work?
2. Did the intended semantic decision really move to the Agent?
3. Are authoritative truth and permissions still deterministic?
4. Are Operational Artifacts still compatible?
5. Can useful intermediate work survive local failure where intended?
6. Is human intervention available at the intended granularity without approval spam?
7. Did Tool, Skill, Harness, Nail, adapter, or retained workflow accidentally recreate contextual orchestration that should belong to the Agent?
8. If a deterministic workflow remains, is its ordering genuinely correctness/capability-bearing?
9. Can the user operate the changed capability primarily through domain intent rather than internal orchestration mechanics?
10. Does the interface explain meaningful progress/consequence instead of merely exposing stage/state/tool transitions?
11. Is enough evidence available for later validation without manufacturing paperwork?

## Exit criteria

Move toward Validate when selected slices are runnable, the intended responsibility transfer can be observed in practice, and the resulting interaction does not unnecessarily push orchestration mechanics back onto the user.

Do not wait for every module to be transformed. Preserve intentionally coarse regions and defer further decomposition when its value does not justify the friction.
