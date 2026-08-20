# Palingen Stage Skills

Palingen uses progressive stage loading rather than one monolithic Skill context.

The root `skills/palingen/SKILL.md` remains the persistent control frame. Detailed stage instructions are intended to be loaded only when entering that stage.

Planned stage skills:

```text
understand/SKILL.md
sediment/SKILL.md
disassemble/SKILL.md
rebuild/SKILL.md
validate/SKILL.md
```

Each stage Skill should eventually define:

- purpose;
- required inputs from previous stages;
- analysis focus;
- Responsibility Map view used in this stage;
- optional supporting tools;
- required output artifacts;
- exit criteria;
- conditions that justify returning to an earlier stage.

## Why staged loading

The intent is not to reproduce a fixed workflow. Staged loading provides cognitive locality:

- the Agent keeps the current problem in focus;
- detailed instructions from later stages do not pollute early analysis;
- each stage produces durable intermediate artifacts;
- human review or intervention can occur at stage boundaries;
- a failed later stage can reuse earlier outputs instead of restarting the entire process.

The stage transition is therefore a **checkpoint and context boundary**, not merely a procedural step number.
