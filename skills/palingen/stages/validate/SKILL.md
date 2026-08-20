# Validate Stage Skill

## Purpose

Use this stage to validate both local Agentification slices and the overall value of the current Agentification iteration, then decide whether to accept, defer further refinement, or return to the smallest relevant earlier stage.

Load:

- `../../references/validation-acceptance.md`
- the current Responsibility Map;
- Harness Mapping;
- Skill / Capability / Glue maps when they exist;
- relevant slice plans and implementation evidence.

Do not treat "the demo ran once" as sufficient validation.

## Validation levels

### 1. Slice Validation

For each meaningful migration slice, verify:

- underlying capability still works;
- operational artifact contracts remain compatible;
- intended semantic decisions actually moved to Agent control;
- Harness boundaries still enforce required truth, policy, authority, and recovery;
- intermediate results remain usable where intended;
- human inspection or intervention exists at the intended granularity;
- no unnecessary micro-Tool, micro-Skill, or adapter explosion was introduced.

If a slice fails, fix or revisit that slice first rather than restarting the whole Agentification process.

### 2. System Validation

At meaningful milestones, compare the current system with the original reasons for Agentification.

Evaluate:

- human attention and interface-switching burden;
- LLM/request-contract and integration burden;
- semantic glue and workflow rigidity;
- recoverability and reuse of intermediate results;
- quality and cost of human intervention;
- original capability and artifact compatibility;
- architecture integrity across Agent / Skill / Tool / Harness / Human;
- adaptability to new tools, targets, and irregular outputs;
- token, latency, reliability, observability, and maintenance costs.

Prefer concrete behavior and evidence over architecture aesthetics.

### 3. Final Acceptance

Ask whether the objectives of this Agentification iteration have been achieved well enough to stop.

Choose exactly one outcome:

```text
ACCEPT
ACCEPT_WITH_DEFERRED_REFINEMENT
NOT_ACCEPTED
```

#### ACCEPT

Use when the intended value is achieved and no important unresolved issue justifies more work now.

#### ACCEPT_WITH_DEFERRED_REFINEMENT

Use when the iteration achieved its goals but some coarse boundary, known friction, or assumption is intentionally left for future evidence-driven refinement.

If useful, leave only a lightweight `.agentification.md` note with current boundaries, known compromise, and revisit triggers.

#### NOT_ACCEPTED

Use when important compatibility, responsibility, safety, recovery, usability, or value goals were not achieved.

Return to the smallest relevant scope:

```text
local issue              -> Slice
Harness boundary issue   -> Sediment
responsibility issue     -> Disassemble
suitability/value issue  -> Understand / Gate 0
```

Do not restart the full process by default.

## Human acceptance

Do not turn final validation into a long sequence of low-value approvals.

Summarize:

- what materially changed;
- what remained compatible;
- what user pain improved;
- important residual risks or deferred boundaries;
- the recommended acceptance outcome.

Request human judgment only when ownership, business value, or unresolved high-impact ambiguity requires it.

## Stop rule

> Agentification is complete when marginal refinement is no longer justified, not when every component has been transformed.

A valid result may therefore intentionally retain large deterministic blocks and deferred boundaries.

## Expected outputs

Produce a concise validation artifact such as `VALIDATION.md` or equivalent containing:

- relevant Slice Validation results;
- System Validation summary;
- Final Acceptance outcome and rationale;
- deferred refinements and revisit triggers, if any.

The exact format may vary by project. Do not create reporting complexity that exceeds the value of the Agentification itself.
