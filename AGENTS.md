# AGENTS.md — Palingen

Palingen is a research-first project about **Agentification**: transforming existing software into agent-friendly systems by redistributing responsibility between Agent, Skill, Tool, Harness, and Human.

## Current phase

The project is in architecture / methodology research. Do not prematurely turn it into a large framework.

## Working thesis

> Move semantic uncertainty upward to the Agent; move execution truth downward into the Harness.

## When working in this repository

1. Preserve the distinction between **capability** and **workflow**.
2. Prefer classifying an existing responsibility before implementing a new abstraction.
3. Do not introduce an LLM provider layer whose primary job is for fixed code to call a model and parse its output.
4. Do not hide fixed workflows inside Skills merely by rewriting them as prose.
5. Keep deterministic operations deterministic.
6. Treat security, permissions, immutable scope, state integrity, evidence integrity, and auditability as Harness concerns.
7. Preserve raw evidence before semantic interpretation.
8. Keep proposed runtime integrations portable across Agent hosts where practical.
9. Record open architectural questions in `docs/RESEARCH.md` rather than resolving them through accidental implementation choices.

## Conceptual responsibility map

```text
Agent   -> semantic reasoning, adaptation, composition, next-step decisions
Skill   -> domain knowledge, strategy, heuristics, evaluation guidance
Tool    -> deterministic capability
Harness -> invariants, state, events, permissions, evidence, recovery
Human   -> judgment or execution that cannot/should not be automated
```

## Avoid

- framework-first design;
- unnecessary provider wrappers;
- universal semantic normalizers without evidence they are needed;
- moving deterministic correctness logic into prompts;
- allowing an Agent to silently rewrite execution truth;
- conflating tracing with durable state;
- assuming maximum autonomy is the goal.

## Preferred research workflow

```text
Observe existing system
        ↓
Discover responsibilities
        ↓
Classify
        ↓
Identify control-flow ownership
        ↓
Identify semantic glue
        ↓
Identify invariants
        ↓
Propose Agent / Skill / Tool / Harness allocation
        ↓
Validate against concrete examples
        ↓
Only then implement reusable abstractions
```
