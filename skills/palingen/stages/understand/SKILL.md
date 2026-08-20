# Understand Stage Skill

## Purpose

Understand the existing system before changing control ownership.

Before full analysis, run **Gate 0: Agentification Suitability Assessment** using `../../references/suitability-assessment.md`.

Palingen must be willing to conclude that a project should not be Agentified.

## Gate 0 — Suitability first

Check whether material semantic orchestration exists through:

- an LLM in the workflow/decision loop;
- natural-language, semi-structured, probabilistic, or unstable outputs requiring interpretation;
- humans providing semantic glue across deterministic tools.

If none are materially present, prefer ordinary software improvement and stop the Agentification path.

Record one outcome:

```text
NOT_AGENTIFICATION
TOOLCHAIN_AGENTIFICATION
LLM_WORKFLOW_AGENTIFICATION
UNCERTAIN
```

For `TOOLCHAIN_AGENTIFICATION`, target the surrounding semantic orchestration rather than unnecessarily rewriting stable tools.

## Understand focus

Once Gate 0 passes, study:

- entry points and control flow;
- state/data flow;
- side effects and external dependencies;
- domain rules and error/recovery paths;
- LLM call sites and model-response handling;
- semantic parsers, adapters, retries, fallbacks, and normalizers;
- human intervention and attention-switching points;
- operational intermediate/final artifacts and their consumers;
- existing capabilities worth preserving;
- contract-friction hotspots.

Maintain:

```text
What the code DOES
vs.
What the code DECIDES
```

Do not prematurely decompose stable deterministic regions.

## Contract Friction

When collaboration friction is material, load `../../references/contract-friction.md`.

Classify only enough to guide later decisions across:

```text
Transport
Syntax / Format
Schema
Lifecycle
Semantic
Intent / Social
```

Consider Volatility, Opacity, Risk, and Frequency where useful.

Do not assume friction implies Agent mediation. Prefer the lowest-cost resolution that fits the problem.

## Responsibility view

Create the initial Responsibility Map at system/module granularity.

Identify:

- sequencing owners;
- state/truth owners;
- semantic interpretation owners;
- side-effect owners;
- permission/invariant owners;
- human roles;
- mixed-responsibility hotspots;
- semantic-orchestration hotspots.

This is reconnaissance, not final allocation.

## Suggested output

Produce a compact understanding artifact containing:

- Gate 0 outcome and rationale;
- exact project/workflow/toolchain boundary being Agentified;
- major control and state structure;
- semantic-orchestration hotspots;
- contract-friction hotspots and likely treatment direction;
- important existing capabilities;
- operational artifacts/contracts that must remain usable;
- human-intervention/attention hotspots;
- initial Responsibility Map;
- areas explicitly recommended to remain ordinary software.

## Exit criteria

Do not enter Sediment until the Agent can answer:

1. Why is this an Agentification problem rather than ordinary refactoring?
2. What exact boundary is being Agentified?
3. Which parts should clearly remain deterministic conventional software?
4. Where does semantic orchestration currently live?
5. Which operational artifacts/capabilities must not be broken?
6. Which friction is semantic enough to justify later Agent mediation, and which should remain deterministic?
