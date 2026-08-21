# Palingen

> **Agentification for existing software.**

Palingen is a lightweight methodology and Skill set for rebuilding existing software around an Agent-first control model.

The goal is not to replace deterministic software with prompts. It is to redistribute responsibility:

```text
Agent   -> semantic interpretation, contextual decisions, composition
Skill   -> reusable strategy and domain knowledge
Tool    -> deterministic capability
Harness -> execution truth, constraints, permission, evidence, recovery
Human   -> authority and valuable judgment
```

> Move semantic uncertainty upward to the Agent; move execution truth downward into the Harness.

## Three layers

Palingen should be understood at three different layers.

```text
1. Methodology
   How to reason about Agentification.

2. Engineering Skill
   How an Agent applies that methodology to a real repository.

3. Agentified product / tool
   The software experience produced after responsibility has been redistributed.
```

These layers should not expose the same vocabulary to the same audience.

The methodology may use concepts such as Sediment, Responsibility Map, Harness, and Agentification Slice. The Skill may use them internally while working. The resulting product should normally speak the user's domain language instead of requiring users to operate Palingen's internal model.

A concrete Agentified tool may still contain deterministic workflows. Palingen does not ban workflow; it challenges **unnecessary workflow ownership**.

If ordering is genuinely part of correctness, regulation, transaction safety, protocol behavior, or the capability itself, a Tool may keep that workflow internally and expose it as one coarse deterministic capability.

What Palingen tries to remove is accidental orchestration that forces fixed code—or the human—to decide semantic next steps that should remain contextual.

## What Agentification means

Traditional software often mixes capability execution with workflow sequencing, semantic parsing, retries, human glue, and LLM-specific adapters.

Palingen asks two questions first:

```text
What does the code DO?
What does the code DECIDE?
```

Then it preserves stable capabilities, moves contextual semantic decisions toward the Agent, keeps hard correctness and authority boundaries deterministic, and rebuilds only the parts whose responsibility actually needs to change.

The intended result is:

> **Code provides capabilities, not unnecessarily rigid workflows.**

## Method

Palingen v1 uses five reasoning scopes:

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

- **Understand** — discover control, state, semantics, side effects, human glue, and reusable capability.
- **Sediment** — establish what must remain deterministic and authoritative.
- **Disassemble** — separate capability, knowledge, semantic decisions, glue, authority, and obsolete workflow structure.
- **Rebuild** — migrate the smallest valuable responsibility slices.
- **Validate** — verify that the new control structure actually improves adaptability without sacrificing reliability, recoverability, or interaction quality.

The stages are checkpoints and reasoning scopes, not a workflow engine and not a user-facing wizard.

## The living spine: Responsibility Map

The main analytical artifact is the **Responsibility Map**.

Palingen reasons in terms of responsibility atoms:

```text
Decision
Action
Truth
Knowledge
Permission
```

Typical ownership direction:

```text
Decision   -> Agent / deterministic policy / Human
Action     -> Tool / Code
Truth      -> Harness
Knowledge  -> Skill / Reference
Permission -> Harness / Human
```

Other maps and reports are optional views. Create a durable artifact only when it must survive a context, human-review, execution, or future-reuse boundary.

## Long-running work

Long Agentification runs may cross sessions, context windows, authentication changes, tool failures, or human intervention.

Palingen therefore supports a deliberately small **run-state whiteboard** that records enough state to recover the work without encoding the workflow itself.

> **Whiteboard remembers the run; it does not own the run.**

Human interaction should default to **autonomous + reviewable**: ordinary bounded decisions proceed, important conclusions remain inspectable, and blocking requests are reserved for authority, irreversibility, important evidence gaps, or human-only capability.

Progress should be reported when something meaningful changes, not simply because Palingen moved between internal stages.

## Optional domain semantic seeding

Palingen can optionally harvest business vocabulary, concepts, rules, states, outcomes, relationships, aliases, and provenance during Agentification.

This is an experimental sidecar for future cross-project semantic alignment and ontology work.

```text
Project vocabulary
      ↓
Domain Semantic Seed
      ↓ repeated projects
Shared Domain Ontology
      ↓ only if justified
Formal OWL / SHACL / reasoning
```

Palingen v1 does **not** require OWL or ontology tooling.

Semantic seeding defaults to off and should not block a normal Agentification run.

## Target experience

An Agentified system should not merely replace a form or DAG with a chat window while keeping the same mechanical interaction burden.

The desired experience is:

```text
Human states intent / constraints / corrections
                ↓
Agent interprets and composes
                ↓
Harness preserves truth and hard boundaries
                ↓
Tools execute deterministic capability
                ↓
Human sees meaningful progress, consequences, and decisions
```

Internal stages, Tool identifiers, workflow states, retry policies, or approval gates should remain internal unless the user benefits from seeing or controlling them.

A useful test is:

> If the user still has to understand and operate the internal orchestration model, did Agentification actually remove non-goal work?

## Core principles

- Agent owns semantic composition.
- Deterministic work remains deterministic.
- Deterministic workflows may remain inside capabilities when their ordering is intrinsically meaningful.
- Harness owns execution truth, not business workflow sequencing.
- Skills teach; they do not secretly own the workflow.
- Preserve raw evidence before interpretation.
- Prefer the largest safe unit of reuse.
- Split where uncertainty, risk, recovery value, or human judgment makes the boundary useful.
- One attention surface may coordinate many execution surfaces.
- Let the Agent compress the view, never the truth.
- Local failure should not erase useful completed work.
- Minimize non-goal work for the human.
- Internal structure should increase reliability without becoming user-visible ceremony.
- Architectural purity is not the goal; responsibility correction is.

## Repository structure

```text
skills/palingen/SKILL.md
    Root control frame — keep active during a Palingen run.

skills/palingen/stages/
    Understand / Sediment / Disassemble / Rebuild / Validate.

skills/palingen/references/
    Specialized decision guidance loaded only when relevant.

docs/
    Motivation, methodology overview, research backlog, known weaknesses.

experimental/ontology/
    Non-authoritative ontology experiments.
```

Start with [`skills/palingen/SKILL.md`](skills/palingen/SKILL.md).

For the conceptual overview, see [`docs/AGENTIFICATION.md`](docs/AGENTIFICATION.md).

## Non-goals

Palingen v1 is not:

- a workflow DAG engine;
- an LLM provider SDK;
- a universal Agent runtime;
- a mandatory MCP layer;
- a fixed Event Store / State Store architecture;
- a reason to rewrite stable deterministic software;
- a requirement to model every project with an ontology;
- a requirement that every end user understand Agent / Skill / Harness terminology.

## Status

**v1 methodology complete; field validation in progress.**

The next priority is to run Palingen on materially different real projects, observe failure modes, and simplify or strengthen the method only where real friction justifies it.
