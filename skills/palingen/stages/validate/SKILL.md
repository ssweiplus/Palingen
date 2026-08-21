# Validate Stage Skill

## Purpose

Validate local Agentification slices, system-level value, and the stop decision. Accept, defer further refinement, or return to the smallest relevant earlier scope.

Load the original Gate 0 / Understand rationale and project boundary, then use references only when relevant:

- `../../references/validation-acceptance.md`
- `../../references/target-form.md`
- `../../references/execution-truth.md`
- `../../references/human-role.md`
- `../../references/skill-layering.md`
- `../../references/connection-model.md`

Use current Responsibility Map and any other artifacts that actually exist. Do not require missing Harness/Skill/Glue/Connection maps merely for validation paperwork.

Do not treat “the demo ran once” as sufficient validation.

## 1. Slice Validation

For each meaningful migrated slice, verify what is material:

- underlying deterministic capability still works;
- Operational Artifact contracts remain compatible;
- intended semantic decisions actually moved to Agent control;
- truth, authority, permission, and recovery constraints remain deterministic where required;
- Agent interpretation cannot silently replace Fact State;
- useful intermediate results survive local failure where intended;
- human intervention occurs at the intended mode/granularity;
- Skills provide know-how without owning truth, authority, or hidden global sequencing;
- structural Nails do not recreate ordinary workflow sequencing;
- stable deterministic friction has not been needlessly moved to Agent reasoning;
- no unnecessary micro-Tool, micro-Skill, adapter, or hidden workflow was introduced.

If a slice fails, revisit that slice first.

## 2. System Validation

At a meaningful milestone, compare the current system with the original reason for Agentification.

Evaluate only the dimensions relevant to the project, such as:

- human attention and interface-switching burden;
- integration / target-specific adapter burden;
- semantic glue and workflow rigidity;
- recoverability and reuse of intermediate work;
- quality/cost of human intervention;
- original capability and artifact compatibility;
- Agent / Skill / Tool / Harness / Human responsibility integrity;
- adaptability to new tools, targets, or irregular outputs;
- progressive disclosure and traceability of raw evidence;
- token, latency, reliability, observability, or maintenance cost where material.

Use `target-form.md` directionally, not as an architecture-purity checklist.

## 3. Final Acceptance

Choose one:

```text
ACCEPT
ACCEPT_WITH_DEFERRED_REFINEMENT
NOT_ACCEPTED
```

### ACCEPT

The intended value is achieved and no important unresolved issue justifies more work now.

### ACCEPT_WITH_DEFERRED_REFINEMENT

This iteration achieved its goal, while some coarse boundary, known friction, or assumption is intentionally deferred until evidence justifies reopening it.

### NOT_ACCEPTED

Important compatibility, responsibility, safety, recovery, usability, or value goals were not achieved.

Return to the smallest relevant scope:

```text
local implementation / connection issue -> Rebuild / active Slice
Harness / execution-truth issue          -> Sediment
responsibility / Skill-boundary issue    -> Disassemble
suitability / value issue                -> Understand / Gate 0
```

Do not restart the full process by default.

## Human acceptance

Summarize what changed, what stayed compatible, which original friction improved, material residual risks, and the recommended outcome.

Request human judgment only when business value, authority, ownership, or unresolved high-impact ambiguity actually requires it.

## Validation evidence

Preserve enough evidence for another Agent or human to understand why the acceptance outcome was chosen.

This may live in the Responsibility Map, run state, implementation/test evidence, issue/notes, or a concise validation artifact.

A separate `VALIDATION.md` is optional, not required.

Do not create reporting complexity that exceeds the value of the Agentification itself.

## Stop rule

> Agentification is complete when marginal refinement is no longer justified, not when every component has been transformed.

A valid result may intentionally retain large deterministic blocks and deferred boundaries.
