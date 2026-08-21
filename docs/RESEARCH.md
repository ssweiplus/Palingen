# Palingen Research Backlog

This document tracks **long-horizon** questions that may matter after Palingen v1 has been exercised on real projects.

It is not normative guidance and not the field-validation TODO list.

- Operational guidance: `skills/palingen/`
- Current weaknesses / field TODOs: `docs/KNOWN_WEAKNESSES_AND_TODOS.md`

Do not create new core abstractions from these questions without repeated project evidence.

## 1. Cross-project semantic governance

Palingen now supports optional Domain Semantic Seeding.

Longer-term questions:

- Which business concepts and relations remain stable across projects in the same domain?
- How should local vocabulary, aliases, provenance, uncertainty, and candidate mappings be retained?
- When do multiple project seeds justify a shared domain ontology?
- How should project-specific concepts map to shared concepts without forced equivalence?
- Can shared semantics help different Agentified projects reuse Skills, evidence, rules, or capabilities?

Working principle:

> Preserve local vocabulary; align shared meaning gradually.

## 2. Formal ontology threshold

Palingen v1 intentionally stops before formal ontology tooling.

Research when the benefits of formalization justify the cost of:

- Turtle/RDF as a canonical exchange form;
- OWL class/property constraints;
- SHACL validation;
- ontology alignment;
- reasoning/inference;
- versioning and provenance across projects.

Formal ontology must remain a semantic sidecar unless real use demonstrates a stronger role. It must not silently become execution truth.

## 3. Runtime portability

Palingen should remain usable across different tool-using Agent environments.

Research the smallest practical assumptions needed for:

- Skill loading;
- deterministic Tool invocation;
- lightweight run-state recovery;
- artifact/evidence references;
- human intervention;
- resumability across sessions.

Avoid introducing a Palingen-specific runtime merely to normalize vendors.

## 4. Deterministic helper tools

Potential helpers include:

- repository inventory;
- LLM call-site discovery;
- parser/retry/fallback hotspot discovery;
- state-write and artifact-path discovery;
- dependency/call graph extraction;
- human-intervention hotspot discovery.

Research which helpers repeatedly save enough Agent/human effort to justify maintenance.

The intended direction is **analysis assistance**, not a Palingen Runtime or Workflow Engine.

## 5. Cross-project learning

Once multiple projects have been Agentified, study whether reusable patterns emerge around:

- repeated responsibility misclassification;
- common semantic-decision types;
- recurring Harness invariants;
- Skill patterns that remain reusable across implementations;
- common friction-resolution choices;
- Agentification Slice shapes;
- human intervention patterns.

This may eventually support example-driven guidance or machine-assisted classification, but should emerge from observed cases rather than a priori scoring.

## 6. Evaluation evidence

Current validation is qualitative.

After enough real runs, investigate whether useful comparable evidence can be collected for:

- reduction in target-specific semantic glue;
- integration effort for a new tool/target;
- resume/recovery success;
- preserved artifact compatibility;
- human context-switching and approval burden;
- handling of unfamiliar but understandable outputs;
- invariant logic accidentally moved into Agent reasoning;
- latency/token/reliability cost introduced by semantic mediation.

Avoid vanity metrics and pseudo-precision.

## 7. Promotion of generated glue

Agent-created one-off deterministic glue may occasionally prove reusable.

Research a lightweight promotion path:

```text
one-off adaptation
    ↓ repeated real use
proven deterministic transformation
    ↓ tests / provenance / stable contract
reusable Tool or utility
```

Promotion should be evidence-driven and should not create a general code-generation subsystem inside Palingen.

## 8. Shared governance semantics

Palingen already uses a small governance vocabulary:

```text
Decision / Action / Truth / Knowledge / Permission
Agent / Skill / Tool / Harness / Human
Nail / Glue / Lubricant / Remove
```

Research whether repeated use reveals missing concepts or relations.

Do not expand this vocabulary merely for taxonomic completeness. A new core concept should clarify responsibility, lifecycle, connection, authority, or recovery in a way existing concepts cannot.

## Working hypothesis

A successful Agentification does **not** maximize Agent autonomy, architectural uniformity, documentation, or ontology depth.

It creates enough shared semantic governance to reason consistently about heterogeneous software, moves semantic uncertainty to the Agent where useful, keeps deterministic execution deterministic, preserves execution truth and human authority, and stops when further refinement is not worth the friction.
