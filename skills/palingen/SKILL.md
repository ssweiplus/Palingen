# Palingen Agentification Skill

## Purpose

Use Palingen to Agentify an existing software project by reallocating responsibility rather than rewriting everything.

Default objective:

> Agentify the selected target using the Palingen methodology.

Do not ask the user to restate this objective. Ask only for information that materially changes scope, authority, or optional behavior.

## Gate 0 — Should this be Agentified?

Before changing architecture, determine whether semantic orchestration is materially part of the problem.

Agentification is usually justified when one or more of these are important:

- an LLM already participates in workflow or decision logic;
- natural-language, semi-structured, probabilistic, or unstable outputs require semantic interpretation;
- humans currently provide semantic glue across multiple deterministic tools.

If ordinary refactoring is enough, recommend ordinary refactoring.

Load `references/suitability-assessment.md` when the boundary is unclear.

## Operating model

```text
Gate 0
  |
  +-- not suitable -> conventional improvement
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

These are reasoning and checkpoint scopes, not a workflow engine and not a user-facing wizard.

Keep this root Skill active. Load only the current Stage Skill and the references needed for the current decision.

## Core invariants

- Code provides capabilities rather than unnecessarily rigid workflows.
- Agent owns semantic interpretation, contextual decisions, and composition.
- Harness owns execution truth, invariants, permissions, evidence semantics, and recovery constraints.
- Skills teach reusable strategy and knowledge; they must not hide mandatory global sequencing.
- Deterministic work stays deterministic.
- A deterministic workflow may remain inside a Tool/Code capability when its ordering is genuinely part of correctness or the capability itself.
- Preserve raw evidence before interpretation or normalization.
- Prefer the largest safe unit of reuse; split only where a boundary creates real value.
- Human escalation is not a substitute for Agent reasoning.
- Automate execution, not process ownership.
- Let the Agent compress the view, never the truth.
- Local failure should not erase valuable completed work.
- Architectural purity is not the goal; responsibility correction is.
- Internal Palingen terminology should not become mandatory user vocabulary.

## Responsibility Map — the living spine

Maintain one primary **Responsibility Map** at the granularity needed for the current work.

Responsibility atoms:

```text
Decision   — what should happen?
Action     — what operation is performed?
Truth      — what is authoritative / what actually happened?
Knowledge  — what reusable know-how guides decisions?
Permission — who may authorize or constrain an action?
```

Default directions:

```text
Decision   -> Agent / deterministic policy / Human
Action     -> Tool / Code
Truth      -> Harness
Knowledge  -> Skill / Reference
Permission -> Harness / Human
```

Ownership may be layered:

```text
semantic choice -> Agent
execution       -> Tool
execution truth -> Harness
permission      -> Harness / Human
know-how        -> Skill
```

Load `references/responsibility-allocation.md` when ownership is ambiguous.

## Artifact rule

Do not mechanically produce a document for every stage or map type.

> Create a durable artifact only when it carries information that must survive a context boundary, human-review boundary, execution boundary, or future-reuse boundary.

The Responsibility Map is the default long-lived analytical artifact. Harness/Skill/Glue/Connection views, Slice Plans, semantic seeds, and reports are conditional.

## Long-running work and interaction

For work that may cross sessions or context limits, preserve a minimal run-state whiteboard sufficient to recover the target, boundary, current stage/focus, durable progress, blocker or human request, last checkpoint, and next intent.

> Whiteboard remembers the run; it does not own the run.

Use `references/run-state.md` for recovery/state design and `references/interaction-contract.md` for startup, progress, human intervention, recovery, and result presentation.

Default human interaction posture is **autonomous + reviewable**. Block only when authority, irreversibility, important evidence deficiency, or human-only capability requires it.

User-facing updates should normally use domain language and meaningful changes rather than Palingen stage names, internal enums, Tool identifiers, or routine stage-transition reports.

## Optional domain semantic seeding

At startup, semantic seeding may be offered once as an optional experimental capability.

Default to **off**. The offer must not block normal Agentification; if the user does not enable it, continue without semantic seeding.

When enabled, harvest only useful business concepts, terminology, rules, states, outcomes, relations, aliases, and provenance. Do not let the seed become execution truth or a prerequisite for Agentification.

Do not enable it opportunistically later merely because interesting vocabulary appears unless the user explicitly opts in.

Load `references/domain-semantic-seeding.md` only when enabled.

## Reference map

Load by problem, not by habit:

```text
Suitability / Gate 0                 -> suitability-assessment.md
Responsibility ownership             -> responsibility-allocation.md
Harness boundary                     -> harness-mapping.md
Execution truth / artifact semantics -> execution-truth.md
Contract friction                    -> contract-friction.md
Skill extraction / layering          -> workflow-to-skill.md / skill-layering.md
Semantic or generated glue           -> semantic-glue-migration.md / ephemeral-glue.md
Human role                           -> human-role.md
Owner-to-owner connection            -> connection-model.md
Target form                          -> target-form.md
Validation / stop decision           -> validation-acceptance.md
Long-run recovery                    -> run-state.md
Human-facing interaction             -> interaction-contract.md
Optional business semantics          -> domain-semantic-seeding.md
```

## Stages

Detailed guidance lives under `stages/`:

- `understand/SKILL.md`
- `sediment/SKILL.md`
- `disassemble/SKILL.md`
- `rebuild/SKILL.md`
- `validate/SKILL.md`

Return to the smallest relevant earlier scope when new evidence invalidates an assumption. Stop refining when further change no longer justifies its friction.
