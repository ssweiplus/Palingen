# Palingen Stage Skills

Palingen uses progressive stage loading rather than one monolithic Skill context.

The root `skills/palingen/SKILL.md` remains the persistent control frame. Load detailed instructions only for the current stage and only the references relevant to the current problem.

Current stage skills:

```text
understand/SKILL.md
sediment/SKILL.md
disassemble/SKILL.md
rebuild/SKILL.md
validate/SKILL.md
```

The stages form a reasoning/checkpoint structure, not a rigid workflow engine:

```text
Gate 0
  |
  v
Understand
  |
  v
Sediment <-> Disassemble
               |
               v
            Rebuild
               |
               v
            Validate
               |
        accept / defer / return
```

Each stage defines:

- purpose;
- required inputs from prior durable artifacts;
- local analysis focus;
- Responsibility Map view used at that stage;
- references loaded only when relevant;
- outputs needed by later stages;
- exit criteria;
- conditions that justify returning to the smallest relevant earlier scope.

## Cross-stage artifact flow

Prefer a small set of durable artifacts rather than copying all previous reasoning into context.

Typical flow:

```text
Understand
  -> Gate 0 rationale / project understanding / initial Responsibility Map

Sediment
  -> Harness Mapping / authority and high-level Skill boundaries

Disassemble
  -> refined Responsibility Map / capability and Skill candidates /
     workflow-glue analysis / candidate Agentification Slices

Rebuild
  -> runnable slices / lightweight Slice Plans / implementation evidence

Validate
  -> Slice Validation / System Validation / Final Acceptance
```

Optional artifacts such as Skill Map, Connection Map, Glue Map, or `.agentification.md` should exist only when they clarify a real boundary or deferred decision.

## Why staged loading

The intent is not to reproduce a fixed workflow. Staged loading provides cognitive locality:

- the Agent keeps the current problem in focus;
- later-stage detail does not pollute early analysis;
- durable artifacts carry truth and decisions across context boundaries;
- human review or intervention can occur where valuable without requiring approval at every stage;
- later failure can reuse earlier work instead of restarting the entire process;
- feedback returns to the smallest relevant scope rather than restarting by default.

A stage transition is therefore a **checkpoint and context boundary**, not simply a procedural step number.
