# Agentification Methodology Overview

This document is a conceptual overview of Palingen v1.

The normative operating guidance lives in:

```text
skills/palingen/SKILL.md
skills/palingen/stages/
skills/palingen/references/
```

Do not duplicate detailed stage or reference rules here.

## Definition

> **Agentification** is the architectural regeneration of existing software by reallocating semantic decisions, deterministic capabilities, execution truth, knowledge, and authority to the actors best suited to own them.

It is not “add an LLM to the workflow”.

The central inversion is:

```text
Traditional
Code owns workflow + semantic branching
        ↓
Agentification
Agent owns semantic composition
Tool/Code owns deterministic action
Harness owns execution truth and constraints
Skill owns reusable know-how
Human retains authority and valuable judgment
```

A useful shorthand is:

> **Migrate responsibility, not files.**

## Why this exists

Rigid automation works well when inputs, outputs, sequencing, and contracts are stable.

It becomes expensive when systems accumulate:

- semantic `if/else` branches;
- parsers for irregular or changing results;
- LLM-output normalization glue;
- target-specific adapters;
- hard-coded retry/recovery chains;
- human operators manually coordinating heterogeneous tools;
- valuable intermediate outputs hidden inside long workflows.

Palingen does not assume all of this should move to an Agent. It first asks which friction is deterministic and which is genuinely semantic.

## Responsibility model

Palingen reasons with five responsibility atoms:

```text
Decision   — what should happen?
Action     — what operation is performed?
Truth      — what is authoritative / what actually happened?
Knowledge  — what reusable know-how guides decisions?
Permission — who may authorize or constrain an action?
```

Typical ownership:

```text
Decision   -> Agent / deterministic policy / Human
Action     -> Tool / Code
Truth      -> Harness
Knowledge  -> Skill / Reference
Permission -> Harness / Human
```

These assignments are a reasoning language, not a schema every function must satisfy.

## The five reasoning scopes

```text
Gate 0
  |
  +-- ordinary refactoring is enough -> stop
  |
  v
Understand
  v
Sediment <--> Disassemble
  v
Rebuild
  v
Validate
```

### Understand

Recover how the current system actually works: control/state flow, side effects, domain rules, human glue, operational artifacts, semantic interpretation hotspots, and stable capability worth preserving.

Keep asking:

```text
What does the code DO?
What does the code DECIDE?
```

### Sediment

Identify what must remain correct even if the Agent is wrong: authoritative facts, permissions, hard lifecycle constraints, evidence preservation, recovery requirements, and irreversible side-effect controls.

Sediment does not mean “put the workflow into Harness”.

### Disassemble

Selectively separate the old structure into:

```text
stable capability       -> Tool / Code
reusable know-how       -> Skill / Reference
semantic interpretation -> Agent
truth / invariant       -> Harness
human authority         -> Human / Harness boundary
incidental friction     -> deterministic lubricant
obsolete workflow glue  -> Delete
```

Prefer coarse reuse. Split only where uncertainty, authority, recovery, or independent intermediate value makes the boundary useful.

### Rebuild

Reconstruct side-by-side where practical.

The preferred unit is an **Agentification Slice**: the smallest valuable responsibility transfer that can run and be validated without forcing a full rewrite.

A slice often joins:

```text
a deterministic capability
+ a semantic decision boundary
+ the relevant truth / artifact / authority boundary
```

### Validate

Validate more than demo success:

- did semantic control move to the intended owner?
- did deterministic reliability remain deterministic?
- are evidence and truth recoverable?
- can local failure preserve useful completed work?
- is human attention reduced rather than converted into approvals?
- did integration/semantic glue actually decrease?
- is further refinement worth the friction?

Stop when additional decomposition no longer creates enough value.

## Connection language

When owner-to-owner connections are unclear, Palingen may classify them as:

```text
Nail       -> hard truth / safety / authority / lifecycle structure
Glue       -> semantic or contextual composition
Lubricant  -> deterministic representation or transport adaptation
Remove     -> obsolete connection from the old workflow
```

> Use nails for structure, not sequencing.

This is diagnostic vocabulary, not a required connection inventory.

## Execution truth

Keep these distinct:

```text
Fact State      -> authoritative
Working State   -> Agent hypothesis / current strategy
Narrative State -> presentation to humans
```

Raw and operational evidence must remain reachable behind Agent summaries.

> **Let the Agent compress the view, never the truth.**

Palingen does not require Event Sourcing, JSONL, a particular database, or any specific observability backend.

## Human interaction

Default posture:

```text
Autonomous + Reviewable
```

The Agent proceeds on bounded/recoverable decisions. Important conclusions remain inspectable and overrideable. Blocking intervention is reserved for authority, irreversibility, important evidence deficiency, or human-only capability.

## Long-running recovery

Long tasks should preserve a very small run-state whiteboard containing enough information to recover the work across context/session interruption:

```text
target / current boundary
current stage and focus
accepted durable progress
current blocker or human request
last useful checkpoint
next intent
```

It must not become a scheduler or hidden state machine.

> **Whiteboard remembers the run; it does not own the run.**

## Artifact discipline

The Responsibility Map is the default living analytical artifact.

Other maps or reports are conditional.

> Create a durable artifact only when it carries information that must survive a context, human-review, execution, or reuse boundary.

## Optional domain semantic seeding

Palingen may optionally harvest domain vocabulary and relationships during Agentification:

```text
local project vocabulary
        ↓
Domain Semantic Seed
        ↓ repeated projects
Shared Domain Ontology
        ↓ only if justified
formal OWL / SHACL / reasoning
```

The seed is experimental and non-authoritative. Palingen v1 does not require ontology tooling.

## Core principles

1. Code provides capabilities, not unnecessarily rigid workflows.
2. Agent owns semantic composition.
3. Harness owns execution truth and hard constraints, not business sequencing.
4. Skills teach knowledge and strategy; they do not disguise workflow ownership.
5. Deterministic work stays deterministic.
6. Preserve raw evidence before interpretation.
7. Prefer the largest safe reuse boundary.
8. Split where uncertainty becomes operationally valuable.
9. One attention surface may coordinate many execution surfaces.
10. Automate execution, not process ownership.
11. Local failure should not erase valuable completed work.
12. Architectural purity is not the goal; responsibility correction is.
13. Minimize non-goal work for the human.
14. Stop when further refinement is no longer worth the friction.

## Current status

Palingen v1 is complete enough for real-project trials.

The primary remaining work is empirical: observe misclassification, artifact explosion, Skill/Harness regression into hidden workflow, human-attention failures, Slice granularity problems, and recovery friction across materially different projects.
