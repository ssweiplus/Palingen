# Harness Mapping Reference

Use this reference during the **Sediment** stage to identify which responsibilities from an existing project should move downward into the Harness.

The central rule is:

> Move downward everything that must remain true even if the Agent is wrong: raw evidence, authoritative state, invariants, permissions, lifecycle constraints, and recovery structure.

Harness does not own the business workflow. It owns the conditions under which any workflow remains truthful, authorized, observable, and recoverable.

---

## 1. Sediment Map

```text
                    ┌──────────────────────────┐
                    │      Original Project    │
                    │                          │
                    │ workflow / parser /      │
                    │ state / retry / auth /   │
                    │ logs / reports / ui /    │
                    │ permissions / rules      │
                    └─────────────┬────────────┘
                                  │
                                  │ responsibility decomposition
                                  ▼
         ┌─────────────────────────────────────────────────────────────┐
         │                     Sedimentation Split                     │
         └───────────────┬───────────────────────┬─────────────────────┘
                         │                       │
                         ▼                       ▼
              ┌──────────────────┐    ┌────────────────────────┐
              │  rises to Agent  │    │   sinks to Harness     │
              │                  │    │                        │
              │ semantic meaning │    │ authoritative truth    │
              │ strategy         │    │ state                  │
              │ dynamic decision │    │ invariants             │
              │ composition      │    │ permissions            │
              │ interpretation   │    │ lifecycle              │
              │                  │    │ events / artifacts     │
              └──────────────────┘    │ checkpoint / recovery │
                                      └───────────┬────────────┘
                                                  │
                                                  ▼
                                      ┌────────────────────────┐
                                      │        Harness         │
                                      │                        │
                                      │ State Store            │
                                      │ Event Store            │
                                      │ Artifact Store         │
                                      │ Policy Engine          │
                                      │ Human Approval Points  │
                                      │ Checkpoint / Resume    │
                                      │ Tool Invocation Bound. │
                                      └────────────────────────┘
```

---

## 2. Existing-project responsibility to Harness mapping

```text
Original project responsibilities
        │
        ├── raw logs / stdout / stderr / responses
        │        └──────────────▶ Artifact Store
        │
        ├── session state / run state / current stage / branch info
        │        └──────────────▶ State Store
        │
        ├── audit logs / execution history / retries already done
        │        └──────────────▶ Event Store
        │
        ├── permission checks / scope limits / dangerous-operation rules
        │        └──────────────▶ Policy Engine
        │
        ├── approval steps / manual confirmation points
        │        └──────────────▶ Human Approval Gateway
        │
        ├── pause / resume / restart / recover-from-midpoint logic
        │        └──────────────▶ Checkpoint & Recovery
        │
        ├── tool call wrapper / side-effect boundary
        │        └──────────────▶ Tool Invocation Boundary
        │
        └── immutable objective / fixed scope / evidence integrity
                 └──────────────▶ Harness Invariants
```

---

## 3. Mapping table

| Existing responsibility | Typical old form | Harness destination | Why it sediments |
| --- | --- | --- | --- |
| Raw input / raw response / CLI output / logs | print statements, in-memory values, scattered files | Artifact Store | Original evidence must survive interpretation failures |
| Current session / run / stage / branch state | workflow-local variables | State Store | Execution must be resumable and inspectable |
| Executed actions / retry history / actor / timestamps | debug log, ad hoc DB rows | Event Store | Process history must be auditable and replayable |
| Original objective / scope / immutable constraints | prompt text, config, workflow constants | Invariants | Agent drift must not silently rewrite task truth |
| Permission checks / dangerous-operation restrictions | if/else in workflow code | Policy Engine | Safety and authority must not depend on probabilistic reasoning |
| Approval points / manual confirmations / credential provision | informal operator steps | Human Approval Gateway | Human authority must be explicit and recoverable |
| Pause / resume / retry-from-point / branch | restart whole workflow or manual reconstruction | Checkpoint & Recovery | A local failure must not erase successful intermediate work |
| Tool invocation wrapper / parameters / side-effect recording | embedded workflow logic | Tool Invocation Boundary | Execution truth and side effects need a deterministic boundary |

The physical implementation may be simple. A small project may satisfy these responsibilities with files such as:

```text
.state.json
events.jsonl
artifacts/
policy.yaml
```

Do not require heavyweight infrastructure merely because the conceptual Harness has multiple responsibilities.

---

## 4. What should NOT sediment into the Harness

Harness must not become a renamed workflow engine.

| Existing responsibility | Prefer | Avoid putting into Harness because |
| --- | --- | --- |
| Complex business strategy | Agent / Skill | It depends on context and meaning |
| Interpretation of irregular CLI or natural-language output | Agent + low-level Skill | It is semantic rather than authoritative truth |
| Dynamic choice of next capability | Agent | It is contextual sequencing |
| Product-specific operating experience | Skill | It is know-how rather than an invariant |
| Fixed end-to-end business workflow | Agent composition, with only necessary lifecycle constraints in Harness | Hard-coding it recreates the old control structure |
| Target-specific semantic parser that changes frequently | Agent or temporary glue; encode only after the contract stabilizes | The contract is too volatile to justify rigid code |

A useful shorthand is:

```text
Harness sediments:
truth + state + invariants + authority + lifecycle constraints + recovery

Harness does not sediment:
meaning + strategy + semantic interpretation + contextual sequencing
```

---

## 5. Harness decision types

Not all decisions belong to the Agent.

```text
Semantic Decision
  "What does this failure mean?"
  "What should we try next?"
        -> Agent

Mechanical Decision
  retry_count >= limit
  invalid state transition
  missing required evidence
        -> Harness

Authority Decision
  production write
  destructive action
  scope expansion
        -> Harness policy and/or Human
```

Use this distinction to prevent both over-agentification and over-hardcoding.

---

## 6. Three state layers

When migrating state from the old system, distinguish:

### Fact State — Harness authoritative

Examples:

- session id actually returned by the target;
- tool exit code;
- artifact id;
- current run state;
- approval already granted;
- action already executed.

### Working State — Agent-managed hypothesis

Examples:

- likely root cause;
- current strategy;
- current interpretation;
- candidate next action.

### Narrative State — presentation only

Examples:

- "The authentication token probably expired."
- "The previous two steps succeeded and the third is blocked."

Do not allow Working State or Narrative State to overwrite Fact State silently.

---

## 7. Required Sediment artifact: HARNESS_MAPPING.md

The Sediment stage should produce a project-specific `HARNESS_MAPPING.md` or equivalent structured artifact.

Recommended shape:

```md
# Harness Mapping

## 1. Raw Evidence
- source:
  - CLI stdout in scanner.py
  - HTTP responses in api_client.py
- target:
  - Artifact Store
- rationale:
  - Original execution evidence must be preserved before interpretation.

## 2. Execution State
- source:
  - current_task in workflow.py
  - session_id in auth_flow.py
- target:
  - State Store
- rationale:
  - Required for resumability and branch continuity.

## 3. Permission Boundaries
- source:
  - admin checks in action_runner.py
  - environment restrictions in config.py
- target:
  - Policy Engine
- rationale:
  - Risky actions must not depend on probabilistic reasoning.
```

For each mapping, preserve at least:

- source responsibility and code/location evidence;
- proposed Harness destination;
- why this must remain deterministic or authoritative;
- any Human authority involved;
- unresolved ambiguity that must be revisited during Disassemble.

---

## 8. Exit questions for the Agent

Before leaving Sediment, the Agent should be able to answer:

1. Which facts in the old system must remain authoritative after Agentification?
2. Which state must survive pauses, failures, or Agent restarts?
3. Which old checks represent true invariants or authority boundaries rather than workflow sequencing?
4. Which intermediate results must remain independently reusable after a later step fails?
5. Which human interventions are actually approvals or authority boundaries and therefore need explicit representation?
6. Which current workflow decisions must NOT be copied into the Harness because they are semantic or contextual?

If those answers are unclear, the Harness boundary is not yet stable enough to proceed.
