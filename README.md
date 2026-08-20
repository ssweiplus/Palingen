# Palingen

> **Agentification for existing software.**
>
> Turn rigid workflows into agent-friendly systems by moving semantic control to agents and moving invariants into a stable harness.

`[agentification]` `[agentic-architecture]` `[harness]` `[control-inversion]` `[software-refactoring]` `[tool-first]` `[skill-first]` `[event-sourcing]`

---

> **Solve et coagula** — dissolve, then recombine.
>
> **As above, so below.** — used here as a design metaphor: high-level intent should remain traceable to low-level, verifiable capability and evidence.

Palingen takes its name from **palingenesis**: rebirth through reconstruction. The project studies how existing software can be decomposed and rebuilt around an agentic control model rather than merely having an LLM added on top.

## Thesis

**Agentification** is the architectural refactoring process of redistributing pre-programmed control flow, semantic interpretation, and cross-component glue from traditional software to an Agent, while pushing verifiable capabilities, state, constraints, permissions, and evidence down into a stable Harness.

In short:

```text
Traditional software

Code
 ├─ owns control flow
 ├─ calls LLMs
 ├─ parses model output
 ├─ adapts external systems
 ├─ branches on semantic meaning
 └─ stitches components together

                ↓  Agentification

Agent
 ├─ understands intent
 ├─ chooses capabilities
 ├─ interprets irregular results
 ├─ adapts sequencing
 ├─ supplies semantic glue
 └─ decides what to do next

Harness
 ├─ exposes deterministic capabilities
 ├─ preserves state and evidence
 ├─ enforces invariants and permissions
 ├─ records events
 ├─ supports pause / resume / replay
 └─ keeps execution auditable
```

The key change is **control inversion**:

> The code no longer has to know every valid workflow in advance. The Agent owns semantic composition; the Harness owns execution truth.

## Core principles

### 1. Code provides capabilities, not workflows

Prefer reusable, deterministic operations over hard-coded end-to-end sequences.

```text
Before: login -> create session -> send -> parse -> retry -> score
After:  credential.inspect / session.create / message.send / evidence.record
```

The Agent composes capabilities according to context.

### 2. Agent owns semantic glue

Irregular CLI output, changing response formats, ambiguous errors, strategy selection, and context-dependent branching are often better handled by an Agent than by an expanding forest of parsers and `if/else` branches.

This does **not** mean moving all logic into an LLM. Deterministic work should remain deterministic.

### 3. Harness owns invariants

The Agent may choose *how* to proceed, but it should not be trusted to redefine execution truth.

Examples of Harness-owned invariants:

- immutable objectives and scope;
- permissions and approval boundaries;
- append-only evidence;
- state transitions;
- artifact integrity;
- audit events;
- resumability and checkpoints.

### 4. Skills provide strategy, not hidden control flow

A Skill should carry domain knowledge, heuristics, evaluation guidance, and operating strategy. It should not merely disguise a fixed workflow as prose.

```text
Skill = soft control / knowledge
Harness = hard control / invariants
Agent = semantic decision maker
Tool = deterministic capability
```

### 5. Normalize transport, not semantics

A tool result may have a small stable envelope while preserving its raw payload.

```text
ToolResult
├─ ok
├─ raw
├─ metadata
├─ artifacts
├─ warnings
└─ error
```

Avoid forcing every external system into a deep universal semantic schema when an Agent can often interpret the raw result directly.

### 6. Preserve raw before normalize

Original responses, command output, files, human actions, and generated glue should be retained before interpretation or summarization.

### 7. Everything important should be resumable

Agent execution may pause for humans, authentication, external systems, or later continuation. State, events, and artifacts should make recovery possible without relying on conversational memory alone.

## The emerging architecture

```text
                         Agent
                           │
                 ┌─────────┴─────────┐
                 │                   │
               Skills             Context
                 │                   │
                 └─────────┬─────────┘
                           ▼
                    Harness Kernel
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
       Tool Runtime     State/Event      Human Gateway
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                        Artifacts
```

A minimal Harness may eventually contain:

```text
ToolRegistry
StateStore
EventStore
ArtifactStore
TaskManager
PolicyEngine
Sandbox / Runtime
```

## Refactoring lens

Palingen will study existing code through categories such as:

| Existing code | Likely destination |
|---|---|
| Deterministic capability | Tool |
| Environment-specific deterministic adapter | Tool / Driver |
| Domain knowledge and heuristics | Skill |
| Semantic branching and interpretation | Agent |
| Fixed workflow sequencing | Candidate for decomposition |
| Security / correctness invariant | Harness / Policy |
| Persistent execution state | Harness State / Events |
| Raw output and evidence | Artifact Store |
| Human-only action | Human Gateway |

A central research question is not simply **"Can this be done by an Agent?"** but:

> **Who should own this decision, and where should the truth live?**

## Working transformation model

```text
Discover
   ↓
Classify
   ↓
Cut
   ↓
Expose
   ↓
Constrain
   ↓
Skillify
   ↓
Persist
   ↓
Validate
```

This is intentionally provisional. Palingen starts as a research and design project before becoming an implementation framework.

## Non-goals, for now

Palingen is **not** intended to begin as:

- another general-purpose LLM SDK;
- another workflow DAG engine;
- an OpenAI-compatible API wrapper;
- a mandatory MCP framework;
- a framework that replaces deterministic software with prompts;
- a single-vendor Agent runtime.

The goal is to develop a reusable method for transforming existing software into **agent-friendly software**.

## Research directions

Current questions include:

- What code should become a Tool, Skill, Harness invariant, or Agent responsibility?
- What code should never be agentified?
- How do we measure semantic uncertainty, determinism, and risk when assigning responsibility?
- How should fixed workflows be converted into strategy without losing correctness?
- Which parsers and adapters can disappear once the Agent becomes semantic glue?
- When should generated one-off glue code be promoted into a reusable Tool?
- How should Agent-created glue run safely inside a sandbox?
- How can the same Harness work across Codex, OpenCode, Claude Code, and other Agent runtimes?
- How do event sourcing, tracing, replay, branching, and human checkpoints fit together?
- How do we measure whether Agentification actually reduced integration cost and complexity?

See [`docs/RESEARCH.md`](docs/RESEARCH.md) for the evolving research backlog.

## Status

**Early research / architecture phase.**

The repository is deliberately a shell while the Agentification model, classification system, Harness boundary, and refactoring methodology are being developed.
