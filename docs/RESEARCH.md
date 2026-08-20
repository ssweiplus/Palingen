# Palingen Research Backlog

This document is intentionally incomplete. It records the questions that should be answered before Palingen hardens into a framework.

## 1. Responsibility classification

Develop a practical decision model for assigning existing code to one of:

- Agent
- Skill
- Tool
- Harness
- Human
- Presentation / interface

Candidate dimensions:

- semantic uncertainty;
- determinism;
- operational risk;
- need for auditability;
- frequency of change;
- environmental variability;
- reversibility;
- cost of failure.

## 2. Workflow decomposition

Study how to transform a fixed workflow into agent-composable capabilities without losing essential ordering constraints.

Questions:

- Which sequencing is accidental and which is invariant?
- How should mandatory preconditions be represented?
- When is a deterministic workflow still the right abstraction?
- Can a workflow be partially agentified?

## 3. Semantic glue

Classify glue code into:

- deterministic glue;
- semantic glue;
- protocol glue;
- generated / ephemeral glue.

Study when parsers, normalizers, format adapters, retry branches, and error classifiers can be replaced by Agent interpretation, and when they should remain code.

## 4. Skillification

Define a transformation from workflow knowledge into Skills.

A Skill should capture:

- purpose;
- applicability;
- strategy;
- heuristics;
- constraints;
- evaluation guidance;
- tool affordances;
- escalation / human guidance.

It should avoid encoding a hidden mandatory workflow unless that ordering is itself an invariant.

## 5. Harness boundary

Define the minimum stable Harness kernel.

Candidate responsibilities:

- Tool Registry
- State Store
- Event Store
- Artifact Store
- Policy Engine
- Human Gateway
- Checkpoint / resume
- Sandbox / runtime

Research the distinction between:

- trace vs event;
- memory vs state;
- state vs artifact;
- policy vs skill guidance;
- tool validation vs semantic interpretation.

## 6. Agent-created glue

Explore a lifecycle:

```text
Unknown integration
      ↓
Agent interprets result
      ↓
Agent generates ephemeral glue
      ↓
Sandbox execution
      ↓
Artifact + event recording
      ↓
Repeated proven use
      ↓
Promotion candidate
      ↓
Reusable deterministic Tool
```

Define promotion criteria, testing, trust, and provenance.

## 7. Event-sourced execution

Investigate whether the Harness should treat events as execution truth and derive current state through reducers.

Desired properties:

- auditability;
- recovery;
- replay;
- branching;
- model replacement experiments;
- regression testing of Agent decisions.

## 8. Human as executor

Model human actions as first-class tasks rather than exceptional UI interruptions.

Possible capability surface:

- human.ask
- human.confirm
- human.execute
- human.select
- human.annotate
- human.provide_secret

Study pause/resume semantics and how human-provided evidence should be preserved.

## 9. Runtime portability

The method should not depend on one Agent vendor.

Initial runtimes of interest:

- Codex
- OpenCode
- Claude Code
- other tool-using coding agents

Research the smallest common contract between an Agent runtime and a Palingen-style Harness.

## 10. Evaluation

Agentification should be measurable rather than purely stylistic.

Candidate metrics:

- glue-code reduction;
- number of target-specific adapters;
- integration effort for a new system;
- unknown-format recovery rate;
- deterministic failure rate;
- human intervention frequency;
- audit completeness;
- resume success rate;
- replayability;
- semantic error rate;
- amount of invariant logic accidentally moved into the Agent.

## Working hypothesis

A successful Agentification does **not** maximize Agent autonomy.

It moves semantic uncertainty upward to the Agent while moving execution truth downward into the Harness.
