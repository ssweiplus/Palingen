# Palingen — Known Weaknesses and TODOs

This is the field-validation backlog for Palingen v1.

It is **not** a second methodology document. Do not promote an item into the core method until repeated project evidence shows that the current guidance is insufficient.

## Priority 1 — Run real projects

The methodology is internally coherent but still under-tested in practice.

Run Palingen end to end on materially different targets, preferably including:

- an existing LLM workflow application;
- a human-operated multi-tool process;
- a mostly deterministic project that Gate 0 should reject;
- a project with long-running recovery and valuable intermediate artifacts;
- two projects in the same business domain for semantic-seed alignment experiments.

Record friction and failure patterns rather than adding abstractions pre-emptively.

## What to watch

### 1. Artifact explosion

Risk: the Agent mechanically creates Understanding, Harness Map, Skill Map, Glue Map, Connection Map, Slice Plan, reports, and other documents.

Current rule:

> Responsibility Map is the primary living analytical artifact. Create another durable artifact only when information must survive a context, review, execution, or reuse boundary.

TODO: verify whether this is strong enough in real runs.

### 2. Stage ritualization

Risk: the five reasoning scopes turn into mandatory sequential paperwork or approval gates.

Watch for duplicated analysis, artificial waiting, one-document-per-stage behavior, or failure to revisit the smallest relevant earlier scope.

TODO: simplify stage guidance further if this appears in practice.

### 3. Responsibility misclassification

Ambiguous boundaries remain judgment-heavy, especially:

```text
Agent vs deterministic policy
Tool vs internal Code
Skill vs Agent reasoning
Harness invariant vs workflow sequencing
Human Judgment vs Agent autonomy
Lubricant vs semantic glue
```

TODO: collect concrete mistakes and build example-driven calibration. Avoid numeric scoring until evidence justifies it.

### 4. Skills regressing into workflows

Risk:

```text
workflow.py
   ->
Step 1 / Step 2 / Step 3 in SKILL.md
```

TODO: verify that Skills teach reusable know-how and explicitly do not own truth, permission, execution, lifecycle invariants, or hidden global sequencing.

### 5. Harness overgrowth

Risk: semantic business sequencing leaks back into Harness under names such as policy, lifecycle, validation, or recovery.

TODO: collect examples and preserve the rule:

> Harness constrains and remembers; it does not choose ordinary semantic business strategy.

### 6. Human attention quality

Risk: the user becomes either an approval machine or is excluded when authority/judgment really matters.

TODO: observe approval fatigue, unnecessary blocking, unsafe autonomy, poor intervention wording, and whether inspect/annotate/redirect/resume feels natural.

### 7. Agentification Slice granularity

Risk: slices become either too large to expose meaningful decisions or so small that Tool/Skill/interface count explodes.

TODO: keep the coarse-first rule and collect examples before formalizing slice-size guidance.

### 8. Long-run recovery

Risk: the run-state whiteboard becomes either too weak to recover work or grows into a task manager/workflow engine.

TODO: test recovery across real session/context interruption and record the minimum state actually needed.

### 9. Domain semantic seeding

Risk: experimental semantic extraction produces noisy implementation vocabulary, false equivalence across projects, or a maintenance burden larger than its value.

TODO:

- test on at least two projects from the same business domain;
- preserve local vocabulary and provenance;
- distinguish candidate alignment from asserted equivalence;
- evaluate whether lightweight YAML/TTL seeds are actually reusable;
- do not introduce OWL/SHACL requirements until repeated evidence justifies them.

### 10. Target-form value

Directional goals such as one attention surface, progressive disclosure, first-class intermediate results, and local-failure recovery still need practical validation.

TODO: measure whether they reduce real human/integration friction rather than merely making the architecture look more agentic.

## Deferred engineering

### Lightweight helper tools

Potentially useful deterministic helpers include repository inventory, LLM-call-site discovery, parser/retry hotspot detection, dependency/call graph extraction, state-write hotspots, and human-intervention hotspot discovery.

Add a helper only when it saves meaningful Agent or human effort in repeated runs.

Do **not** build a Palingen Runtime, Workflow Engine, Agent SDK, or mandatory state backend as a default direction.

### Quantitative scoring

Deferred.

Prefer qualitative classification plus rationale until multiple real projects provide enough evidence for meaningful metrics.

Avoid false precision such as `Agentification Suitability = 76`.

## Research separation

`docs/RESEARCH.md` contains longer-horizon research questions. This file contains concrete v1 weaknesses to observe during field use.

If the same item appears in both, keep detailed exploration in `RESEARCH.md` and only the operational field risk here.

## v1 modification rule

Before changing the core methodology because of a weakness:

```text
Observe the failure
    ↓
Find the smallest broken boundary
    ↓
Try the smallest correction
    ↓
Re-run on a real project
```

> Fix observed friction; do not design around imagined complexity.
