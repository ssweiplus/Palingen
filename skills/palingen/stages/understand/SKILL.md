# Understand Stage Skill

## Purpose

Understand the existing system before changing control ownership.

Before performing full Understand work, run **Gate 0: Agentification Suitability Assessment** using `../../references/suitability-assessment.md`.

Palingen must be willing to conclude that a project should not be Agentified.

## Gate 0 — Suitability first

Determine whether the problem actually contains semantic orchestration that benefits from an Agent.

Check whether:

- an LLM is already part of the application's workflow or decision loop;
- natural-language, semi-structured, probabilistic, or unstable results require semantic interpretation;
- humans currently provide semantic glue across several deterministic tools.

If none of these are materially present, prefer ordinary software improvement and stop the transformation path.

Typical alternatives include:

- dependency/install automation;
- configuration simplification;
- CLI/UI improvements;
- packaging or containers;
- deterministic adapters;
- ordinary modular refactoring.

Do not Agentify merely because software is inconvenient to use.

Record one Gate 0 outcome:

```text
NOT_AGENTIFICATION
TOOLCHAIN_AGENTIFICATION
LLM_WORKFLOW_AGENTIFICATION
UNCERTAIN
```

For `NOT_AGENTIFICATION`, explain the cheaper conventional improvement path rather than forcing a Palingen architecture.

For `TOOLCHAIN_AGENTIFICATION`, treat the semantic orchestration around the tools as the target; do not unnecessarily rewrite stable tools.

For `LLM_WORKFLOW_AGENTIFICATION`, proceed with the project itself as a strong candidate.

For `UNCERTAIN`, inspect only enough to resolve suitability before investing in full analysis.

## Understand focus

Once Gate 0 passes, study:

- entry points;
- control flow;
- state flow;
- data flow;
- external dependencies;
- side effects;
- domain rules;
- error and recovery paths;
- human intervention points;
- LLM call sites and model-response handling;
- semantic parsers, adapters, retries, fallbacks, and normalizers;
- contract friction;
- operational intermediate and final artifacts;
- places where users must switch attention across interfaces.

Maintain the distinction:

```text
What the code DOES
vs.
What the code DECIDES
```

Do not prematurely decompose stable deterministic regions.

## Responsibility view

Create the initial Responsibility Map at system/module granularity.

Identify:

- sequencing owners;
- state owners;
- semantic interpretation owners;
- side-effect owners;
- permission and invariant owners;
- human roles;
- mixed-responsibility hotspots;
- semantic-orchestration hotspots.

This is reconnaissance, not final allocation.

## Suggested output

Produce a compact understanding artifact containing:

- Gate 0 suitability outcome and rationale;
- project/task boundary being Agentified;
- major control and state structure;
- semantic-orchestration hotspots;
- contract-friction hotspots;
- important existing capabilities;
- important intermediate/final artifacts that must remain usable;
- human-intervention hotspots;
- initial Responsibility Map;
- areas explicitly recommended to remain ordinary software.

## Exit criteria

Do not enter Sediment until the Agent can answer:

1. Why is this an Agentification problem rather than ordinary refactoring?
2. What exact boundary is being Agentified: project, LLM workflow, or surrounding toolchain?
3. Which parts should clearly remain conventional deterministic software?
4. Where does semantic orchestration currently live?
5. Which existing artifacts and capabilities must not be broken by the transformation?
