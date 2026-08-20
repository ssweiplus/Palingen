# Agentified Target Form Reference

Use this reference during Rebuild and Validate to judge whether the emerging architecture actually reflects Palingen's intended control structure.

## Core shape

```text
Human
  ↕
One attention surface
  ↕
Agent
  ↕
Skills / Harness
  ↕
Tools and retained deterministic capabilities
  ↕
CLI / API / Browser / services / files
```

> One attention surface, many execution surfaces.

Execution may remain heterogeneous. Human attention should not be forced to fragment across unrelated tools simply because the underlying capabilities differ.

## Semantic I/O vs Execution I/O

Separate:

- **Semantic I/O** — goals, context, evidence, interpretations, decisions, explanations.
- **Execution I/O** — API payloads, CLI flags, browser actions, file formats, protocol details.

The Agent should reason over semantic meaning while Tools and deterministic adapters handle stable execution contracts.

## Intermediate results are first-class

Useful intermediate results should be inspectable, reusable, branchable, and recoverable when their value justifies it.

A local failure should not erase previous successful work.

Prefer execution states that can represent partial progress or waiting, rather than forcing every run into only SUCCESS/FAIL.

## Human process ownership

The human must not be reduced to a retry button or approval machine.

Where useful, support:

```text
inspect / interrupt / edit / branch / reuse / resume
```

Agent automates execution and semantic coordination; the human retains authority over goals and important consequences.

## Progressive disclosure

Default presentation should concentrate attention on:

- current status;
- what materially happened;
- important evidence;
- state/side-effect impact;
- recommended next action or decision.

Raw, structured, and detailed evidence should remain reachable without being dumped into the primary attention surface.

> Let the Agent compress the view, never the truth.

## Capability composition

Tools should expose independently meaningful capabilities rather than hide end-to-end semantic workflows.

Skills should teach strategy and domain knowledge rather than dictate rigid sequencing.

Harness should mediate execution truth, policy, state, observability, and recovery without owning semantic business composition.

Conceptually:

> Agent asks; Harness mediates; Tool acts.

## Failure behavior

Local action failure should allow the system to remain inspectable and recoverable when possible.

Possible conceptual states include:

```text
RUNNING
WAITING_FOR_HUMAN
PARTIALLY_COMPLETE
BLOCKED
FAILED_ACTION
COMPLETED
```

Exact names are implementation-specific.

## Architectural legibility

An Agent or maintainer should be able to discover:

- available capabilities;
- applicable Skills/References;
- Harness invariants and authoritative state;
- human authority/intervention points;
- current execution progress and important evidence.

## Target-form questions

Before accepting the architecture, ask:

1. Is human attention more unified even if execution surfaces remain heterogeneous?
2. Does the Agent actually own semantic composition?
3. Are deterministic capabilities still deterministic?
4. Are intermediate results usable and recoverable where valuable?
5. Can humans intervene without being required to approve everything?
6. Are raw facts traceable behind compressed presentation?
7. Have Tools, Skills, or Harness accidentally recreated the old workflow?
