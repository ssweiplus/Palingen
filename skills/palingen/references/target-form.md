# Agentified Target Form Reference

Use this reference during Rebuild and Validate to judge whether the emerging architecture actually reflects Palingen's intended control structure and produces a naturally operable system.

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

## Do not expose internal orchestration as the product UX

An Agentified system can still feel like a rigid workflow if the user is forced to operate internal stages, states, tool calls, or approval gates directly.

Avoid product experiences such as:

```text
Step 1 complete
Approve Step 2?
Select Tool A or Tool B
Approve tool call
Choose retry policy
Advance workflow stage
```

when those choices can be handled safely by the Agent and Harness.

Prefer domain-oriented interaction:

```text
User expresses intent / constraint / correction
        ↓
Agent interprets and composes capabilities
        ↓
Harness constrains and preserves truth
        ↓
User sees meaningful progress, consequence, and decisions
```

The architecture may be structured internally without making the user operate that structure manually.

> Internal structure should improve reliability, not become user ceremony.

## Workflows are allowed when the domain actually needs them

Palingen does not ban deterministic workflows.

A workflow is appropriate when ordering itself is part of correctness, regulation, transaction safety, or a genuinely fixed business process.

The problem is not the existence of workflow. The problem is exposing accidental implementation sequencing as if it were the user's job or the domain's truth.

Therefore distinguish:

```text
Required workflow
= order is intrinsically meaningful / correctness-bearing

Accidental workflow
= order exists mainly because old software had to pre-encode orchestration
```

Retain the first. Challenge the second.

## User language should be domain language

Internal concepts such as Agent, Harness, Skill, Responsibility Map, Slice, lifecycle state, or tool identifier may be useful to maintainers and advanced users.

They should not dominate the default user surface unless they are themselves part of the user's domain.

Prefer:

```text
"I need you to log in again"
```

over:

```text
"Human Executor required at BLOCKING intervention point"
```

Prefer:

```text
"I am keeping the existing API client and changing only session recovery"
```

over:

```text
"Agentification Slice 2 has entered Rebuild"
```

Methodology vocabulary should remain inspectable without becoming mandatory product vocabulary.

## Intermediate results are first-class

Useful intermediate results should be inspectable, reusable, branchable, and recoverable when their value justifies it.

A local failure should not erase previous successful work.

Prefer execution states that can represent partial progress or waiting, rather than forcing every run into only SUCCESS/FAIL.

## Human process ownership

The human must not be reduced to a retry button or approval machine.

Where useful, support natural forms of:

```text
inspect / interrupt / edit / branch / reuse / resume
```

Agent automates execution and semantic coordination; the human retains authority over goals and important consequences.

Human controls should be expressed in the user's language where practical, for example:

```text
查看当前情况
暂停
补充说明
改变方向
跳过这部分
从这里另开方案
继续
停止
```

rather than requiring the user to understand orchestration primitives.

## Progressive disclosure

Default presentation should concentrate attention on:

- current meaningful status;
- what materially happened;
- important evidence;
- state/side-effect impact;
- recommended next action or decision.

Raw, structured, and detailed evidence should remain reachable without being dumped into the primary attention surface.

> Let the Agent compress the view, never the truth.

Progress updates should follow meaningful change, not every internal transition.

## Capability composition

Tools should expose independently meaningful capabilities rather than hide end-to-end semantic workflows.

Skills should teach strategy and domain knowledge rather than dictate rigid sequencing.

Harness should mediate execution truth, policy, state, observability, and recovery without owning semantic business composition.

Conceptually:

> Agent asks; Harness mediates; Tool acts.

The user should usually interact with the Agent's semantic surface, not directly orchestrate the Tool/Harness relationship.

## Failure behavior

Local action failure should allow the system to remain inspectable and recoverable when possible.

Possible internal states include:

```text
RUNNING
WAITING_FOR_HUMAN
PARTIALLY_COMPLETE
BLOCKED
FAILED_ACTION
COMPLETED
```

Exact names are implementation-specific and do not need to become user-facing labels.

Translate internal state into useful meaning, such as:

```text
"I completed the analysis and code change, but validation is blocked because the target service is unavailable."
```

## Architectural legibility

An Agent or maintainer should be able to discover:

- available capabilities;
- applicable Skills/References;
- Harness invariants and authoritative state;
- human authority/intervention points;
- current execution progress and important evidence.

This legibility does not require exposing the same vocabulary to every end user.

## Target-form questions

Before accepting the architecture, ask:

1. Is human attention more unified even if execution surfaces remain heterogeneous?
2. Does the Agent actually own semantic composition?
3. Are deterministic capabilities still deterministic?
4. Are intermediate results usable and recoverable where valuable?
5. Can humans intervene without being required to approve everything?
6. Are raw facts traceable behind compressed presentation?
7. Have Tools, Skills, or Harness accidentally recreated the old workflow?
8. Does the product force users to understand internal orchestration concepts that could remain internal?
9. Are progress and intervention presented in domain language rather than stage/tool/state jargon?
10. If a fixed workflow remains, is its ordering genuinely required by the domain or correctness rather than inherited accidentally?
11. Can a user state intent, correction, or changed direction naturally without mapping it onto internal workflow controls?

## Principle

> Agentification should remove mechanical orchestration from the human where that orchestration carries no human value.

> A system is not meaningfully Agentified if the Agent is flexible internally but the user still has to operate it like a workflow engine.
