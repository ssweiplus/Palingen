# Validation & Acceptance

Validation in Palingen is layered. Do not apply the same heavyweight checklist to every change.

```text
Validation
├── Slice Validation
│   └── Did this local responsibility migration preserve correctness and boundaries?
├── System Validation
│   └── Did the Agentification create meaningful net value at system level?
└── Final Acceptance
    └── Has this iteration done enough to stop?
```

The goal is not to prove that every component has been Agentified. The goal is to verify that intended responsibilities moved correctly, original capabilities remain usable, user effort decreased, and further refinement is justified only when it still produces meaningful value.

## 1. Slice Validation

Run after a meaningful Agentification slice, not after every trivial edit.

A slice is a small but complete responsibility migration such as:

```text
capability
  -> decision boundary
  -> state / artifact boundary
```

Validate at least:

- the underlying capability still works;
- original operational artifact contracts remain usable;
- semantic decisions intended for the Agent are no longer hidden in workflow code;
- Harness invariants and permission boundaries remain deterministic;
- intermediate results are inspectable or reusable where intended;
- human intervention is possible at the intended decision boundary;
- the slice did not introduce unnecessary Tool, Skill, Harness, or adapter fragmentation.

Slice Validation is primarily correctness plus ownership-boundary validation.

## 2. System Validation

Run at meaningful milestones after several slices or after a coherent Agentification iteration.

Evaluate whether the system is actually better for the reasons that justified Agentification.

### Human attention

Ask:

- Does the user switch between fewer unrelated interfaces?
- Does the Agent absorb installation, configuration, LLM-contract, format-conversion, and cross-tool coordination work where appropriate?
- Has manual work shifted toward meaningful judgment instead of mechanical operation?
- Are users being turned into approval machines?

### Semantic glue

Ask:

- Did semantic parser / adapter / fallback burden decrease?
- Does the Agent now own genuinely contextual interpretation and composition?
- Did stable deterministic glue remain deterministic?
- Did a new universal normalizer appear and merely relocate contract friction?

### Recoverability and intermediate value

Ask:

- Are useful intermediate results preserved and independently usable?
- Can local failure remain local?
- Can execution resume, branch, retry, or redirect without repeating unrelated successful work?
- Are failures and human interventions observable with evidence?

### Compatibility

Ask:

- Do original capabilities still work?
- Are original intermediate and final operational artifacts still consumable by the original software where required?
- Did evidence capture avoid breaking paths, formats, mutation semantics, or downstream consumers?

### Architecture integrity

Ask:

- Are Tools capabilities rather than disguised workflows?
- Are Skills knowledge and strategy rather than rigid sequencing?
- Does Harness protect truth, policy, authority, and recovery without owning unnecessary business workflow?
- Can Agent hypotheses be distinguished from authoritative state?

### Adaptability

Ask:

- Is a new target, tool, output variation, or workflow variant cheaper to integrate?
- Does the system require less pre-encoded semantic glue?
- Can understandable irregular outputs be handled without immediately adding another parser?

### Cost

Also check the negative side:

- model/token cost;
- latency;
- operational reliability;
- additional state or observability complexity;
- maintenance burden of Skills and Harness;
- whether code complexity merely moved into prompts or hidden orchestration.

System Validation asks whether Agentification produced **net value**, not merely whether it runs.

## 3. Final Acceptance

Final Acceptance answers:

> Has this Agentification iteration done enough to stop?

Do not interpret final acceptance as "every possible component has been transformed."

Check at least:

1. Core capabilities and required artifact compatibility are preserved.
2. The original user pain that justified Agentification has materially improved.
3. Semantic orchestration has moved to the intended Agent boundary.
4. Harness preserves the required truth, state, authority, evidence, and recovery guarantees.
5. Valuable intermediate results can be inspected, reused, and recovered where intended.
6. Human intervention occurs where human value or authority is high, without creating unnecessary approval burden.
7. The new structure is easier to adapt or operate than the old one.
8. Remaining friction is either acceptable or explicitly deferred.
9. Further refinement has enough expected benefit to justify its cost.

## 4. Acceptance Outcomes

Use one of three outcomes.

### ACCEPT

The objectives of this Agentification iteration are met and no meaningful unresolved issue justifies further work now.

### ACCEPT_WITH_DEFERRED_REFINEMENT

The objectives of this iteration are met, but some known friction or coarse boundaries remain intentionally deferred.

When useful, record only lightweight follow-up context in `.agentification.md`:

- current boundary;
- known compromise or assumption;
- revisit trigger.

Do not create a heavy continuous-optimization process.

### NOT_ACCEPTED

A core Agentification objective was not achieved or an important compatibility, responsibility, safety, recovery, or usability boundary is wrong.

Return to the smallest relevant level:

```text
local bug / boundary issue  -> relevant Slice
Harness boundary wrong      -> Sediment
responsibility split wrong  -> Disassemble
value assumption wrong      -> Understand / Suitability
```

Do not restart the entire process by default.

## 5. Stop Rule

Palingen follows a lazy refinement principle:

> **Agentification is complete when marginal refinement is no longer justified, not when every component has been transformed.**

Prefer stopping when the important user and architecture gains have been achieved.

Do not continue decomposition merely for architectural purity.

## 6. Validation Summary Template

A lightweight final report may use:

```yaml
slice_validation:
  status: pass | fail | partial
  notes: []

system_validation:
  human_attention: improved | neutral | worse
  semantic_glue: improved | neutral | worse
  recoverability: improved | neutral | worse
  compatibility: preserved | degraded
  architecture_integrity: acceptable | needs_revision
  adaptability: improved | neutral | worse
  cost: acceptable | excessive | unknown

final_acceptance:
  outcome: ACCEPT | ACCEPT_WITH_DEFERRED_REFINEMENT | NOT_ACCEPTED
  rationale: "..."
  deferred:
    - boundary: "..."
      revisit_when: "..."
```

Use evidence and concrete behavior rather than architecture aesthetics when making the final judgment.
