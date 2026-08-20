# Palingen Agentification Skill

## Purpose

Use this Skill to transform an existing software project into an agent-friendly system through the Palingen Agentification methodology.

Palingen does not prescribe one fixed workflow implementation. It provides a staged reasoning method, responsibility-allocation protocol, and supporting references/tools. The Agent remains the semantic orchestrator.

## Gate 0 — Decide whether to Agentify at all

Before entering the five-stage process, first ask whether the target is actually an Agentification problem.

Use `references/suitability-assessment.md` and prefer ordinary software improvement when semantic orchestration is not materially part of the problem.

Agentification is usually justified when at least one of the following is materially present:

- an LLM is already embedded in the application's workflow or decision loop;
- natural-language, semi-structured, probabilistic, or unstable outputs require semantic interpretation;
- humans currently provide semantic orchestration across multiple deterministic tools.

If none of these are present, recommend conventional engineering instead of forcing Agentification.

> Agentification is justified by semantic orchestration, not by software inconvenience alone.

> If ordinary refactoring is enough, prefer ordinary refactoring.

Palingen must be able to recommend **do not Agentify**.

## Core operating model

After Gate 0 passes:

1. Understand
2. Sediment
3. Salvage / Disassemble
4. Rebuild
5. Validate

Sediment and Disassemble may iterate. Rebuild should migrate the smallest valuable responsibility slices. Validate may return to the smallest relevant earlier scope.

```text
Gate 0
  |
  +-- not suitable --> conventional improvement
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
  +-- accept / defer
  +-- return to smallest broken boundary
```

## Progressive loading

Keep this root Skill as the persistent control frame. Load the current Stage Skill only when entering that stage, then load references only when the corresponding decision is materially present.

Do not load every reference into active context by default.

## Cross-stage invariants

- Preserve original project goals, constraints, observed facts, and operational compatibility where required.
- Code provides capabilities rather than unnecessarily rigid workflows.
- Agent owns semantic composition and contextual decisions.
- Harness owns execution truth, state integrity, permissions, evidence semantics, observability boundaries, and recovery constraints.
- Skills carry knowledge and strategy; they must not disguise fixed workflows as prose.
- Preserve raw evidence before interpretation or normalization.
- Prefer deterministic code for deterministic work.
- One attention surface may coordinate many heterogeneous execution surfaces.
- Concentrate user attention without deleting information.
- Let the Agent compress the view, never the truth.
- Automate execution, not process ownership.
- A failed local action should not erase successful intermediate work.
- Minimize non-goal work for the human; spend machine effort to save human attention.
- Prefer the largest safe unit of reuse; do not decompose stable code for architectural purity.
- Split more finely where uncertainty, risk, valuable intermediate results, or human judgment make an inspection point useful.
- Expose uncertainty without forcing human attention at every decision point.
- Human escalation is not a substitute for Agent reasoning.
- Artifact capture must not break operational artifact use.
- Palingen defines meaningful execution-event semantics, not a mandatory observability backend.

## Core reference map

Load references by problem, not by habit:

```text
Should this be Agentified?        -> suitability-assessment.md
What friction exists?             -> contract-friction.md
Who should own this responsibility? -> responsibility-allocation.md
What must remain true?            -> harness-mapping.md
State/Event/Artifact semantics     -> execution-truth.md
Workflow knowledge extraction     -> workflow-to-skill.md
Semantic glue migration           -> semantic-glue-migration.md
Temporary generated glue          -> ephemeral-glue.md
Human participation               -> human-role.md
What should the rebuilt form be?  -> target-form.md
Validation and stop decision       -> validation-acceptance.md
```

## Responsibility Allocation Protocol

Responsibility allocation is the spine of the process. Maintain a living **Responsibility Map**.

Start by identifying responsibility atoms:

```text
Decision   — what should happen next?
Action     — what operation is performed?
Truth      — what actually happened / is authoritative?
Knowledge  — what reusable know-how guides decisions?
Permission — who may authorize or constrain the action?
```

Default directions:

```text
Decision   -> Agent / deterministic policy / Human
Action     -> Tool / Code
Truth      -> Harness
Knowledge  -> Skill / Reference
Permission -> Harness / Human
```

Use `references/responsibility-allocation.md` when the boundary is ambiguous. Consider Determinism, Semantic Dependency, Contract Volatility, Truth Criticality, Risk/Authority, and Composability.

Ownership may be layered rather than singular:

```text
Intent / semantic choice -> Agent
Execution                -> Tool
Execution truth          -> Harness
Permission               -> Harness / Human
Operational know-how     -> Skill
```

## Stage-level use of the Responsibility Map

### Understand

Identify current sequencing, state, interpretation, side effects, permissions, human roles, contract-friction hotspots, and mixed responsibilities. Do not prematurely assign every function.

### Sediment

Establish the load-bearing boundary: authoritative truth, permissions, invariants, lifecycle constraints, evidence/observability semantics, and recovery descend into Harness; semantic interpretation and contextual strategy remain outside.

### Salvage / Disassemble

Separate reusable deterministic capability, semantic decisions, knowledge, glue, authority, and obsolete workflow-only code. Prefer coarse reuse and split where uncertainty becomes valuable.

### Rebuild

Migrate responsibility rather than files. Use minimal Agentification slices, preserve compatible deterministic blocks, prefer side-by-side reconstruction, and ensure old workflow code no longer secretly owns the semantic decision being transferred.

### Validate

Verify slice correctness, system-level Agentification value, and final acceptance. Stop when further refinement is no longer justified.

## Execution truth

Keep these distinct:

```text
Fact State      -> authoritative
Working State   -> Agent hypothesis / strategy
Narrative State -> presentation
```

Operational artifacts remain usable by their real consumers. Harness evidence capture may reference, snapshot, copy, hash, or record metadata without silently changing artifact contracts.

Meaningful execution changes should be observable through a pluggable boundary. Do not require a particular Event Store, JSONL file, tracing stack, or audit backend.

## Human role

Humans may act as Authority, Judgment, Provider, Executor, Annotator, or Controller.

Prefer the least intrusive useful intervention mode:

```text
autonomous
reviewable / overrideable
blocking only when necessary
```

Humans should be able to inspect, pause, annotate, replace, branch, skip, redirect, and resume where the interaction surface supports it.

## Granularity and incremental refinement

Agentification may be deliberately incomplete in one pass.

Prefer the largest safe reuse boundary. Split more finely only when uncertainty, risk, human judgment, independent intermediate value, or recovery value justifies it.

Do not optimize toward architectural purity.

When useful, leave a lightweight `.agentification.md` containing only:

- current boundaries;
- known compromises/assumptions;
- evidence-based revisit triggers.

## Target-form principles

The rebuilt project should trend toward:

- one attention surface, many execution surfaces;
- Agent-owned semantic composition;
- independently composable deterministic capabilities;
- Harness-owned execution truth/authority/recovery constraints;
- first-class useful intermediate results;
- local failure that does not automatically become global workflow failure;
- progressive disclosure rather than raw-information dumping;
- natural human intervention without approval fatigue;
- architectural legibility: capabilities, Skills, invariants, authority, evidence, and current progress are discoverable.

## Detailed stage guidance

Detailed stage guidance belongs under `skills/palingen/stages/`.

Stage boundaries are checkpoints and context boundaries, not rigid workflow ownership. Revisit earlier artifacts when new evidence changes a boundary, but return to the smallest relevant scope.
