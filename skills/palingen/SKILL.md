# Palingen Agentification Skill

## Purpose

Use this Skill to transform an existing software project into an agent-friendly system through the Palingen Agentification methodology.

Palingen does not prescribe one fixed workflow implementation. It provides a staged reasoning method, responsibility-allocation protocol, and supporting references/tools. The Agent remains the semantic orchestrator.

## Core operating model

Agentification proceeds through five major stages:

1. Understand
2. Sediment
3. Salvage / Disassemble
4. Rebuild
5. Validate

Stages 2 and 3 overlap and may iterate. Do not force a strictly linear pass when discoveries during disassembly change the Harness boundary or Skill structure.

## Progressive stage loading

Do not load all detailed stage instructions into active context at once.

Use this root Skill as the persistent control frame. Load the detailed sub-skill for the current stage only when entering that stage. Complete that stage's required artifacts and exit criteria before loading the next stage, unless a documented feedback loop requires revisiting an earlier stage.

Recommended progression:

```text
Root Palingen Skill
        |
        v
Understand sub-skill
        |
  stage artifacts
        |
        v
Sediment sub-skill
        |       ^
        |       |
        v       |
Disassemble sub-skill
        |
        v
Rebuild sub-skill
        |
        v
Validate sub-skill
```

The root Skill preserves cross-stage invariants; sub-skills provide local reasoning instructions.

## Cross-stage invariants

These rules remain active across every stage:

- Preserve original project goals, constraints, and observed facts.
- Code provides capabilities rather than unnecessarily rigid workflows.
- Agent owns semantic composition and contextual decisions.
- Harness owns execution truth, state integrity, permissions, evidence, and recovery.
- Skills carry knowledge and strategy; they must not merely disguise fixed workflows as prose.
- Preserve raw evidence before interpretation or normalization.
- Prefer deterministic code for deterministic work.
- Concentrate user attention without deleting information.
- Automate execution, not process ownership.
- A failed local action should not erase successful intermediate work.

## Responsibility Allocation Protocol

Responsibility allocation is not a one-time step. It is the spine of the Agentification process and must be revisited at different granularities throughout the stages.

Maintain a living **Responsibility Map** during the engagement.

### System-level view — Understand

Identify broad ownership in the existing system:

- who controls sequencing;
- who owns persistent state;
- who interprets external results;
- who performs side effects;
- who enforces permissions and invariants;
- where humans intervene;
- where contract friction accumulates.

At this stage, mark mixed-responsibility hotspots rather than prematurely assigning every function.

### Architecture-level view — Sediment

Use the Responsibility Map to establish the new load-bearing structure:

- Truth and critical state tend to sediment into the Harness.
- Permission and irreversible boundaries tend to sediment into Harness and/or Human authority.
- Semantic Decisions may rise to the Agent.
- High-level Knowledge becomes high-level Skills.
- Reusable deterministic capability candidates are marked for later exposure as Tools.

This stage defines the proposed ownership boundaries before detailed code salvage.

### Code-level view — Salvage / Disassemble

Decompose mixed functions and modules into responsibility atoms:

- **Decision** — what should happen next?
- **Action** — what operation is performed?
- **Truth** — what actually happened or what state is authoritative?
- **Knowledge** — what recurring know-how or strategy guides decisions?
- **Permission** — who is allowed to authorize or constrain the action?

Map those atoms toward likely owners:

```text
Decision   -> Agent, deterministic policy, or Human depending on context
Action     -> Tool / deterministic code
Truth      -> Harness
Knowledge  -> Skill / reference
Permission -> Harness / Human
```

Also consider Lubricant for small deterministic interface-friction helpers and Delete for glue that exists only because of the old rigid workflow.

### Composition review — Rebuild

Use the Responsibility Map in reverse to detect accidental re-coupling:

- Does a Tool contain hidden semantic decisions?
- Does a Skill encode a rigid workflow that should remain contextual?
- Can the Agent overwrite authoritative state or evidence?
- Does the Harness unnecessarily dictate semantic sequencing?
- Did old parser/adapter glue reappear without independent value?

### Ownership validation — Validate

Compare proposed ownership with observed runtime behavior:

- Did the Agent receive enough context to make semantic decisions?
- Did Harness invariants remain deterministic under Agent error?
- Did Tools remain independently reusable?
- Did Skills provide useful strategy without becoming hidden code paths?
- Could a human inspect, interrupt, modify, branch, reuse, and resume intermediate work?

## Responsibility Map

Keep the Responsibility Map as a persistent project artifact rather than an ephemeral analysis note.

Suggested conceptual fields:

```yaml
- id: auth-expiry-interpretation
  source: path/to/code
  responsibility_atom: Decision
  current_owner: workflow-code
  proposed_owner: Agent
  support_skill: auth-recovery
  harness_constraints:
    - credential state remains authoritative
  rationale:
    determinism: low
    semantic_dependency: high
    contract_volatility: high
    truth_criticality: medium
    risk_authority: medium
    composability: medium
```

The exact storage format may vary by project. Preserve the reasoning and ownership history.

## Detailed stage guidance

Detailed stage guidance belongs in separate sub-skills under `skills/palingen/stages/`.

Until those stage sub-skills are fully specified, use the methodology references in `docs/` and do not invent a rigid end-to-end workflow.
