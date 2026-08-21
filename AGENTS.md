# AGENTS.md — Palingen

Palingen is a lightweight methodology and Skill set for **Agentification**: transforming existing software by redistributing responsibility between Agent, Skill, Tool, Harness, and Human.

## Current phase

Palingen v1 methodology is complete enough for field use. The priority is now real-project validation, not continued abstraction growth.

Do not turn Palingen into a large runtime, workflow framework, ontology platform, or provider SDK unless repeated field evidence clearly requires it.

## Working thesis

> Move semantic uncertainty upward to the Agent; move execution truth downward into the Harness.

## When working in this repository

1. Treat `skills/palingen/SKILL.md` as the root control frame.
2. Load only the active Stage Skill and references relevant to the current decision.
3. Keep the **Responsibility Map** as the primary living analytical artifact.
4. Create other durable artifacts only when they must survive a context, review, execution, or reuse boundary.
5. Preserve the distinction between **capability** and **workflow**.
6. Keep deterministic operations deterministic.
7. Do not hide fixed workflows inside Skills, Tools, Harness, or run-state records.
8. Preserve raw evidence before semantic interpretation.
9. Prefer coarse reuse; split only where uncertainty, authority, recovery, or independent value justifies a boundary.
10. Use the lightweight run-state whiteboard only when long-running recovery is useful.
11. Keep human interaction autonomous + reviewable by default; block only when authority or evidence requires it.
12. Treat domain semantic seeding as optional, experimental, and non-authoritative.
13. Record unresolved field questions in `docs/KNOWN_WEAKNESSES_AND_TODOS.md` or `docs/RESEARCH.md` rather than creating new core abstractions prematurely.

## Responsibility model

```text
Agent   -> semantic reasoning, contextual decisions, composition
Skill   -> reusable knowledge, strategy, heuristics
Tool    -> deterministic capability
Harness -> truth, invariants, permission, evidence, recovery
Human   -> authority and valuable judgment
```

Responsibility atoms:

```text
Decision / Action / Truth / Knowledge / Permission
```

## Avoid

- framework-first design;
- workflow engines disguised as Harness;
- numbered workflow prose disguised as Skills;
- universal semantic schemas without field evidence;
- treating event sourcing or any storage backend as required architecture;
- making run-state a task scheduler;
- generating every possible analysis artifact mechanically;
- moving deterministic correctness logic into prompts;
- using ontology terminology as a prerequisite for ordinary Agentification;
- optimizing for architectural purity instead of reduced human and integration friction.

## Default change test

Before adding a new Palingen concept or mechanism, ask:

```text
Does this clarify lifecycle?
Does this clarify responsibility?
Does this clarify an important connection or recovery boundary?
Is there real project evidence that it is needed?
```

If not, prefer not to add it.
