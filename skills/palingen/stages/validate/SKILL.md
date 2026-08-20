# Validate Stage Skill

## Purpose

Validate local Agentification slices, system-level value, and final acceptance. Decide whether to accept, defer further refinement, or return to the smallest relevant earlier scope.

Load:

- the original Gate 0 / Understand rationale and project boundary;
- `../../references/validation-acceptance.md`;
- `../../references/target-form.md`;
- `../../references/execution-truth.md` when State/Event/Artifact behavior is material;
- `../../references/human-role.md` when intervention quality is material;
- `../../references/skill-layering.md` when Skill integrity is material;
- `../../references/connection-model.md` when important connection choices were introduced;
- current Responsibility/Harness/Skill/Capability/Glue/Connection artifacts and Slice Plans as applicable.

Do not treat "the demo ran once" as sufficient validation.

## 1. Slice Validation

For each meaningful migration slice, verify:

- underlying capability still works;
- Operational Artifact contracts remain compatible;
- evidence capture did not interfere with artifact use;
- intended semantic decisions actually moved to Agent control;
- Harness still enforces truth, policy, authority, and recovery constraints;
- Agent Working/Narrative State cannot silently replace Fact State;
- meaningful execution changes remain observable without depending on a specific backend;
- intermediate results remain usable where intended;
- human intervention exists at the intended mode/granularity;
- Skills provide know-how without owning truth, authority, or hidden global sequencing;
- Nails protect structural correctness rather than recreating workflow sequencing;
- semantic Glue is visible where intended and stable deterministic friction remains Lubricant/Code;
- no unnecessary micro-Tool, micro-Skill, adapter, connection layer, or hidden workflow was introduced.

If a slice fails, revisit that slice first.

## 2. System Validation

At meaningful milestones, compare the current system with the original Gate 0 / Understand reasons for Agentification.

Evaluate:

- human attention and interface-switching burden;
- LLM/request-contract and integration burden;
- semantic glue and workflow rigidity;
- recoverability/reuse of intermediate work;
- quality and cost of human intervention;
- original capability and Operational Artifact compatibility;
- architecture integrity across Agent / Skill / Tool / Harness / Human;
- connection integrity across Nail / Glue / Lubricant / Remove decisions where material;
- adaptability to new tools, targets, and irregular outputs;
- progressive disclosure and traceability of raw evidence;
- token, latency, reliability, observability, and maintenance costs.

Use `target-form.md` as a directional check, not as an architecture-purity checklist.

Prefer concrete behavior and evidence over aesthetics.

## 3. Final Acceptance

Ask whether the objectives of this Agentification iteration have been achieved well enough to stop.

Choose exactly one:

```text
ACCEPT
ACCEPT_WITH_DEFERRED_REFINEMENT
NOT_ACCEPTED
```

### ACCEPT

Use when intended value is achieved and no important unresolved issue justifies more work now.

### ACCEPT_WITH_DEFERRED_REFINEMENT

Use when this iteration achieved its goals but some coarse boundary, known friction, or assumption is intentionally left for evidence-driven refinement.

If useful, leave a lightweight `.agentification.md` with current boundaries, known compromise, and revisit triggers.

### NOT_ACCEPTED

Use when important compatibility, responsibility, safety, recovery, usability, or value goals were not achieved.

Return to the smallest relevant scope:

```text
local implementation / connection issue -> Slice / Rebuild
Harness / execution-truth issue          -> Sediment
responsibility / Skill-boundary issue    -> Disassemble
suitability / value issue                -> Understand / Gate 0
```

Do not restart the full process by default.

## Human acceptance

Do not turn final validation into approval spam.

Summarize what changed, what stayed compatible, which original pain improved, material residual risks, and the recommended outcome.

Request human judgment only when ownership, business value, authority, or unresolved high-impact ambiguity actually requires it.

## Stop rule

> Agentification is complete when marginal refinement is no longer justified, not when every component has been transformed.

A valid result may intentionally retain large deterministic blocks and deferred boundaries.

## Expected output

Produce a concise `VALIDATION.md` or equivalent containing:

- relevant Slice Validation results;
- System Validation summary against original Agentification rationale;
- Final Acceptance outcome and rationale;
- deferred refinements/revisit triggers, if any.

Do not create reporting complexity that exceeds the value of the Agentification itself.
