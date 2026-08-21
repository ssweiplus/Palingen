# Palingen Stage Skills

Palingen uses stage Skills for **cognitive locality**, not to encode a fixed workflow.

Keep `../SKILL.md` active as the root control frame. Load one Stage Skill when that reasoning scope becomes relevant, then load only the references needed for the current decision.

```text
Gate 0
  |
  v
Understand
  v
Sediment <--> Disassemble
  v
Rebuild
  v
Validate
  |
  +-- accept / defer / return to smallest broken boundary
```

Stage Skills:

```text
understand/SKILL.md
sediment/SKILL.md
disassemble/SKILL.md
rebuild/SKILL.md
validate/SKILL.md
```

## What each stage is for

- **Understand** — discover the current control/state structure and semantic-orchestration hotspots.
- **Sediment** — establish truth, authority, invariant, evidence, and recovery boundaries.
- **Disassemble** — decide what remains capability, what becomes knowledge, what moves to Agent control, and what old glue disappears.
- **Rebuild** — migrate the smallest valuable Agentification Slices without unnecessary decomposition.
- **Validate** — test slice correctness, system-level value, recoverability, and the stop decision.

Sediment and Disassemble may iterate. Validate may return directly to the smallest relevant earlier scope.

## Artifact discipline

Do **not** create one document per stage by default.

The primary living analytical artifact is the **Responsibility Map**.

Create another durable artifact only when information must survive a context, review, execution, or reuse boundary.

Typical durable information may include:

```text
Understanding / boundary rationale
Responsibility Map
critical Harness or authority decisions
active Slice implementation evidence
validation evidence
minimal run state for long tasks
optional Domain Semantic Seed
```

Harness Maps, Skill Maps, Glue Maps, Connection Maps, Workflow Extractions, and Slice Plans are optional views. Create them only when they materially clarify a decision or carry information forward.

## Stage transition rule

A stage transition is a checkpoint/context boundary when useful, not an approval gate.

Do not wait for artificial “stage completion” if useful work can continue safely. Do not ask the human to approve every transition.

Checkpoint only enough accepted truth, evidence, and intent to avoid repeating valuable work.
