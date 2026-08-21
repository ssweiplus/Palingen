# Palingen Research Backlog

This document tracks open research questions after the Palingen v1 methodology was formed.

It is **not** the normative specification for Palingen. Current operational guidance lives in `skills/palingen/`.

Several earlier ideas have now been intentionally narrowed:

- Harness is a responsibility boundary, not a required bundle of Event Store / Artifact Store / workflow-engine components.
- Execution events are semantic observability signals; Palingen does not require event sourcing or one event backend.
- Operational Artifacts must remain compatible with their real consumers; evidence capture may reference/snapshot/hash/copy without hijacking the original artifact contract.
- Skills carry knowledge and strategy; they do not own execution truth, authority, or hidden global sequencing.
- Agentification should prefer coarse reuse and minimal responsibility transfer over architecture-purity rewrites.

## 1. Real-project validation

The highest-priority research task is to run Palingen v1 end-to-end on real projects.

Observe:

- whether stages improve reasoning or become ceremony;
- whether too many analysis artifacts are created;
- where Responsibility / Skill / Harness boundaries are repeatedly misclassified;
- whether Agentification Slices are naturally sized in practice;
- whether human intervention becomes useful or approval-heavy;
- whether original capability and artifact compatibility remain intact;
- whether semantic glue is actually reduced rather than merely moved into prompts.

Prefer evidence from repeated use over adding new methodology concepts.

## 2. Artifact discipline

Palingen has several possible views and artifacts, but most should remain optional.

Research a practical rule for when an analysis deserves durable storage.

Working principle:

> Create a durable artifact only when it carries information needed across a context boundary, for human inspection, or for later execution/recovery.

The Responsibility Map is currently the strongest candidate for the primary living analysis artifact. Harness Mapping, Skill Map, Glue Map, Connection Map, Workflow Extraction, and other views should remain conditional.

## 3. Responsibility allocation quality

The v1 model uses responsibility atoms plus six dimensions:

- Determinism;
- Semantic Dependency;
- Contract Volatility;
- Truth Criticality;
- Risk / Authority;
- Composability.

Research where this model is insufficient or ambiguous across real projects.

Do not introduce numeric scoring until repeated cases show that numbers improve decisions.

## 4. Skill degradation

A major risk is converting rigid workflow code into rigid workflow prose.

Study:

- which Skill patterns preserve strategy without owning sequencing;
- whether `does_not_own` materially prevents responsibility creep;
- when Procedure Fragments are helpful vs disguised workflows;
- how Skill boundaries evolve when domain knowledge stabilizes.

## 5. Harness boundary drift

Monitor whether Harness responsibility gradually expands from:

```text
truth + authority + invariants + observability semantics + recovery
```

into business sequencing or strategy.

Research practical warning signs and review heuristics for this drift.

Do not prescribe a fixed Harness infrastructure stack.

## 6. Human intervention economics

The v1 model distinguishes:

```text
autonomous
reviewable / overrideable
blocking
```

Research which conditions reliably justify each mode and how to avoid approval fatigue while preserving real human authority.

## 7. Agentification Slice granularity

Rebuild uses Agentification Slice as the main migration unit.

Study:

- when a slice is too coarse to expose useful semantic control;
- when it is too fine and creates micro-Tools/micro-Skills;
- whether capability + semantic decision + state/artifact boundary is sufficient as a recurring pattern;
- how side-by-side migration behaves in larger systems.

## 8. Deterministic helper tools

Palingen should remain a Skill/methodology rather than harden into a heavy framework.

Potential low-risk helpers include:

- repository inventory;
- LLM call-site discovery;
- parser / retry / fallback hotspot search;
- state-write and artifact-path discovery;
- dependency / call graph extraction;
- human-intervention hotspot discovery.

Research which helpers genuinely save Agent/human effort before adding them.

Avoid creating a Palingen runtime, workflow engine, or mandatory SDK without strong evidence.

## 9. Domain Semantic Seeding

Palingen v1 now reserves an experimental path for low-cost business-semantic harvesting.

See `skills/palingen/references/domain-semantic-seeding.md`.

Research:

- which business concepts/relationships are worth retaining;
- how to separate implementation vocabulary from durable domain semantics;
- how provenance should be represented;
- how local vocabularies from multiple projects can be aligned without forced equivalence;
- when repeated semantic seeds justify a shared domain ontology;
- when Turtle / OWL / SHACL or reasoning provides enough value to justify formalization.

Working principle:

> Preserve local vocabulary; align shared meaning gradually.

The semantic seed is a sidecar and must not become execution truth.

## 10. Runtime portability

The methodology should remain usable across different tool-using coding/Agent environments.

Research the smallest practical assumptions Palingen makes about an Agent runtime without creating a Palingen-specific runtime dependency.

## 11. Evaluation

Current validation uses qualitative Slice / System / Final Acceptance rather than a numerical score.

Potential future evidence may include:

- reduced integration/glue burden;
- fewer target-specific semantic adapters;
- successful resume/recovery;
- preserved artifact compatibility;
- reduced human context switching;
- reduced approval burden;
- ability to handle irregular but understandable outputs;
- amount of invariant logic accidentally moved into Agent reasoning.

Do not optimize for vanity metrics such as number of Agent calls, number of Skills, code deleted, or automation percentage.

## Working hypothesis

A successful Agentification does **not** maximize Agent autonomy or architectural uniformity.

It creates a shared governance language for heterogeneous software, moves semantic uncertainty to the Agent where useful, keeps deterministic execution deterministic, preserves execution truth and human authority, and stops when further refinement is not worth the friction.
