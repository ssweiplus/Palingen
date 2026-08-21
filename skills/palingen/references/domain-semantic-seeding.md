# Domain Semantic Seeding Reference

## Status

Experimental, non-authoritative, optional.

Use this reference when an Agentification engagement reveals business vocabulary, entities, rules, states, outcomes, or relationships that may be useful across future projects in the same domain.

The goal is not to build a complete ontology during v1. The goal is to cheaply preserve semantic material that may later support ontology alignment.

> Capture semantics cheaply before deciding whether to formalize them deeply.

> Preserve local vocabulary; align shared meaning gradually.

## Why this exists

Different projects in the same business domain often encode similar concepts using different names, structures, prompts, UI labels, schemas, or workflow branches.

Palingen should not force those projects into one implementation shape. It may, however, preserve enough business semantics that later projects can be aligned in a shared semantic space.

Example:

```text
Project A: 问题项
Project B: Finding
Project C: 违规记录

        ↓ candidate alignment

Shared concept candidate: ReviewFinding
```

The original project terms remain valid and traceable.

## Separation from Palingen core semantics

Palingen core semantics describe Agentification governance:

```text
Agent / Skill / Tool / Harness / Human
Decision / Action / Truth / Knowledge / Permission
```

Domain semantics describe the business world of the project:

```text
business object
business concept
business action
business state
business rule
business outcome
business relationship
```

Do not confuse the two.

A drawing-review assistant and a coding assistant should usually produce different domain semantic seeds even though both are governed by the same Palingen core semantics.

## What to harvest

Collect only material that appears useful and reasonably grounded.

Candidate categories:

- important business concepts and entities;
- business objects/artifacts;
- business actions;
- business states;
- business rules and constraints;
- outcomes/findings/conclusions;
- meaningful relationships;
- local aliases and terminology variants;
- candidate mappings to previously known concepts.

Avoid harvesting every identifier, class, table, or field merely because it exists.

## Provenance first

Every meaningful semantic assertion should remain traceable to its source when practical.

Useful provenance includes:

- source file / code location;
- prompt or Skill text;
- UI label;
- schema or API field;
- business document;
- human clarification;
- existing project artifact.

Suggested lightweight record:

```yaml
id: review-finding
kind: concept
label: 审查问题
aliases:
  - 问题项
  - finding
source:
  - src/review/result.py
confidence: high
```

For relationships:

```yaml
subject: review-finding
predicate: violates
object: review-rule
source:
  - src/review/evaluator.py
```

`confidence` is descriptive only. Do not turn it into a pseudo-scientific scoring system.

## Candidate alignment, not forced equivalence

When another project uses a similar concept, preserve uncertainty explicitly:

```text
candidateEquivalentTo
relatedTo
broaderThan
narrowerThan
possiblySameAs
```

Do not silently collapse two domain concepts merely because their labels look similar.

Shared domain ontology should emerge from repeated evidence across projects.

## Maturity path

```text
Level 0 — Raw Vocabulary
    terms discovered in code / prompts / UI / docs

Level 1 — Semantic Seed
    concepts + relations + provenance + aliases + candidate mappings

Level 2 — Shared Domain Ontology
    stable cross-project vocabulary and relationships

Level 3 — Formal Ontology
    OWL / SHACL / reasoning only if repeated use justifies it
```

Palingen v1 targets Level 1 at most.

## Output form

Do not require OWL in v1.

A project may use compact YAML, Markdown, JSON, Turtle, or another lightweight representation if semantic preservation is useful.

If a machine-readable experimental representation is desired, Turtle is preferred over OWL/XML because it is compact, diff-friendly, and easy for humans and Agents to inspect.

## Important boundary

Domain semantic seed is a semantic projection, not execution truth.

```text
source code / business evidence / Harness facts
                 ↓
        semantic interpretation
                 ↓
        Domain Semantic Seed
```

Do not let the ontology seed overwrite authoritative project state, operational artifacts, permissions, or execution evidence.

## When not to create it

Skip domain semantic seeding when:

- the project has little meaningful domain vocabulary;
- no cross-project reuse is expected;
- extraction would create more maintenance burden than value;
- the semantics are too uncertain to record usefully;
- the only concepts discovered are implementation details.

This is an experimental sidecar, not a required Palingen deliverable.
