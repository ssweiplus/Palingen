# Agentification Methodology Draft

> **Agentification** is an architectural regeneration process for existing software: understand the control and state structure of the old system; sediment deterministic, constraint-bearing, and verifiable responsibilities into a stable Harness; lift semantic interpretation, dynamic decision-making, and cross-component composition to an Agent; selectively salvage capabilities and knowledge from the old system; rebuild them under a new control structure; and validate the result through adaptability, reliability, recoverability, and auditability.

Palingen treats Agentification as **rebuilding a house next to an old one**, not as adding an LLM call into existing workflow code.

> **Solve et coagula** — dissolve, then recombine.

The old structure is first understood and separated by responsibility. A new load-bearing structure is then established beside it. Reusable materials and useful knowledge are salvaged from the old structure and reassembled into an agent-friendly system.

---

## 1. Why Agentification

Traditional automation owns most of the control flow in code:

```text
Code
  -> call API / CLI / model
  -> parse output
  -> branch
  -> normalize
  -> retry
  -> call next component
```

This works well when contracts are stable and semantics are deterministic. It becomes expensive when a system must integrate heterogeneous and changing execution surfaces such as:

- APIs
- CLIs
- browser interactions
- SSE / streaming responses
- files
- semi-structured text
- model outputs
- human actions

The implementation then accumulates adapters, parsers, fallback branches, retry chains, target-specific normalization, and semantic `if/else` logic.

The central problem is not merely protocol diversity. It is **contract friction**, especially **semantic contract friction**: the program must decide what an irregular result means and what should happen next.

Agentification changes the ownership of that uncertainty.

```text
Traditional automation

Code owns:
- sequencing
- semantic branching
- output interpretation
- cross-component glue

Agentified system

Agent owns:
- semantic interpretation
- contextual sequencing
- adaptation
- composition

Harness owns:
- execution truth
- state
- constraints
- permissions
- evidence
- recovery
```

The goal is not to replace deterministic code with an LLM. The goal is to place uncertainty and determinism on the sides best suited to handle them.

---

# 2. The Five-Stage Agentification Process

```text
1. Understand
2. Sediment
3. Salvage / Disassemble
4. Rebuild
5. Validate
```

Stages 2 and 3 are intentionally overlapping. While the new structural frame is being designed, discoveries made while dismantling the old system may change what must be placed in the Harness or represented as Skills.

## 2.1 Understand — understand the old house

Before introducing an Agent, understand why the current system works.

Study at least:

- entry points
- control flow
- state flow
- data flow
- external dependencies
- side effects
- domain rules
- error paths
- human intervention points
- hidden coupling

A particularly useful distinction is:

```text
What the code DOES
vs.
What the code DECIDES
```

For example:

```text
send request                 -> does
refresh credential           -> does
create session               -> does

"is this credential expired?" -> decides
"should we refresh now?"      -> decides
"should this operation retry?"-> decides
```

The first group tends to become capabilities. The second group is where Agentification may change control ownership.

This phase is **control-flow archaeology** rather than implementation.

---

## 2.2 Sediment — establish the new load-bearing structure

Before deciding which old code to reuse, decide what the new system must never delegate to probabilistic reasoning.

The metaphor is sedimentation:

```text
       flexible / semantic / contextual
                    ^
              Agent / LLM
          strategy, interpretation,
          composition, adaptation

-----------------------------------------

                  Harness
       state, truth, permissions,
       evidence, lifecycle, recovery
                    v
        stable / deterministic / heavy
```

### Responsibilities that tend to sediment into the Harness

- immutable facts and objectives
- state consistency
- lifecycle transitions
- authorization and permissions
- approval boundaries
- transaction boundaries
- raw evidence preservation
- event history
- checkpoints and recovery
- audit requirements
- irreversible side-effect controls

### Responsibilities that tend to rise into the Agent

- semantic interpretation
- strategy selection
- contextual sequencing
- non-standard output understanding
- exception interpretation
- cross-component composition
- dynamic adaptation
- deciding when human help is required

### High-level Skills also emerge here

Sedimentation is not only about code. High-level Skills belong to the new structural frame.

Examples:

- security assessment
- incident response
- code audit
- data analysis
- release management

A high-level Skill describes:

- the objective of a class of work
- major phases
- important invariants
- what evidence must be preserved
- strategy guidance
- escalation / human-intervention points
- completion and stop conditions

A high-level Skill is closer to the architecture of the new house than to a reused piece of the old one.

---

## 2.3 Salvage / Disassemble — dismantle the old house selectively

Once the new frame is becoming visible, return to the old project and decide what should be carried into the new system.

The question is not simply **"which code can be reused?"**

The better question is:

> **In what form should this old asset be reborn in the new architecture?**

### Building materials — reusable deterministic capabilities

Examples:

- stable SDKs
- HTTP clients
- database access
- cryptographic operations
- schema validators
- file processing
- stable business APIs

Typical destination:

```text
Tool / Runtime Capability
```

### Furniture — reusable knowledge and domain assets

Examples:

- templates
- prompt seeds
- scoring criteria
- domain rules
- error-code knowledge
- operating guidance

Typical destination:

```text
Skill / Resource / Reference
```

### Old structural walls — usually not moved directly

Examples:

- large workflow executors
- state machines containing semantic branching
- target-specific semantic parsers
- hard-coded retry chains
- code whose only purpose is to parse LLM text back into workflow state

Typical treatment:

```text
extract useful capability or knowledge;
do not preserve the old control structure by default
```

### Debris — delete when the new architecture removes the reason it existed

Examples:

- duplicated adapters
- compatibility glue with no independent value
- excessive normalization
- DTOs that exist only to support rigid sequencing
- large sets of semantic `if/else` parsers

### Low-level Skills emerge during disassembly

The old system often contains local experience that is too semantic to become a deterministic Tool but too valuable to discard.

Examples:

- how a particular CLI signals expired authentication
- how to interpret a product-specific diagnostic response
- how to recognize a common false positive
- how to approach an irregular streaming interface

These become low-level or micro Skills, references, or procedure fragments.

Therefore:

```text
High-level Skill  -> organizes a class of work
Low-level Skill   -> helps with a local recurring problem
Tool              -> performs a deterministic capability
Harness           -> preserves structural truth and constraints
```

---

# 3. Three Ways to Join the New System

A useful Palingen design language is to ask whether two parts should be joined with a **nail**, **glue**, or **lubricant**.

## 3.1 Nails — structural coupling

Nails are explicit and strong. They are used where truth and structure matter.

Examples:

- permission checks
- immutable objectives
- lifecycle boundaries
- required approvals
- audit requirements
- state-machine invariants
- high-level Skill constraints

Principle:

> **Use nails for structure, not for unnecessary sequencing.**

Too many nails recreate a rigid workflow under a new name.

## 3.2 Glue — semantic coupling

Glue joins components whose relationship depends on meaning and context.

Typical questions:

- What does this CLI output actually mean?
- Did an HTTP 200 represent business success?
- Which field appears to be the current session identifier?
- Should the existing conversation be resumed or replaced?
- Does this error require retry, recovery, or escalation?

This is where an Agent is valuable.

> **LLM is semantic glue.**

Much traditional glue code is human interpretation encoded prematurely as parsers and branches.

## 3.3 Lubricant — reduce incidental interface friction

Lubricant is different from semantic glue. The two components already conceptually fit; utilities simply make the interaction smoother.

Examples:

- ANSI stripping
- encoding normalization
- JSON formatting
- chunk aggregation
- transport-level SSE parsing
- deterministic schema validation
- caching
- artifact references
- lightweight retry wrappers

Principle:

> **Normalize transport, not semantics.**

A useful summary is:

```text
Structural coupling   -> nails
Semantic coupling     -> Agent glue
Incidental friction   -> lubricant / utilities
```

Or:

> **Rigid where truth matters, fluid where meaning varies.**

---

# 4. Rebuild — compose the new house

The preferred migration model for existing software is usually **side-by-side reconstruction**, not demolition followed by a big-bang rewrite.

```text
Old System                         Agentified System

workflow                           Agent
adapters             ---->         Skills
libraries                          Harness
business APIs                      Tools / Capabilities
```

The new system may initially call stable functions or modules from the old system through Tools. Over time, more responsibilities can be separated.

The intended control inversion is:

```text
Old:
Code -> LLM/API/CLI -> parse -> branch -> next step

New:
Agent -> inspect Skill/State -> invoke capability -> observe -> adapt
                                      ^
                                   Harness
```

The Agent becomes the owner of **semantic composition**.

The Harness remains the owner of **execution truth**.

---

# 5. The Target Form of an Agentified System

Agentification should converge toward a recognizable architectural pattern rather than merely producing "some code with tools".

## 5.1 One attention surface, many execution surfaces

A human should not be required to act as the orchestrator across unrelated interfaces.

```text
                    Human
                      |
                      v
             Interaction Surface
          CLI / Chat / IDE / TUI
                      |
                      v
                    Agent
                      |
                Harness + Skills
                      |
       +--------------+--------------+
       |              |              |
      API            CLI          Browser ...
```

> **One attention surface, many execution surfaces.**

The user's attention is concentrated even though execution remains distributed.

## 5.2 Agent-mediated semantic I/O

All important **human-facing semantic input and output** should be mediated by the Agent.

Humans should primarily express:

- intent
- constraints
- feedback
- approvals
- corrections

And receive:

- what happened
- why it matters
- important evidence
- state impact
- what happens next

This does **not** mean every byte must pass through an LLM.

## 5.3 Execution I/O remains lossless

Machine-facing execution data belongs to the Harness and evidence layer:

- stdout / stderr
- exit codes
- HTTP requests and responses
- headers
- streaming chunks
- files
- screenshots
- timestamps
- tool parameters
- side effects

The Agent may interpret and summarize these facts but must not become their sole representation.

> **LLM owns presentation; Harness owns preservation.**

## 5.4 Progressive disclosure

The system should reduce cognitive load without deleting information.

```text
Agent explanation
      |
Key facts / evidence
      |
Structured execution result
      |
Raw artifact
```

A user sees the most relevant layer first and can inspect deeper layers when necessary.

> **Concentrate attention, not information.**

> **Let the Agent compress the view, never the truth.**

## 5.5 Presentation contract

Agent output should be flexible language, but important semantic slots should not disappear arbitrarily.

For significant actions, the interaction surface should make available:

- status
- what happened
- evidence references
- state impact
- next action / required human action

The exact wording may vary. The underlying facts must remain traceable.

A useful principle is:

> **Structured truth, flexible language.**

---

# 6. Interaction and Execution Planes

A mature Agentified application can be understood as two major planes.

```text
                    Semantic Plane

Human <---------> Agent
                  reasoning
                  planning
                  interpretation
                  presentation

------------------------------------------------

                    Execution Plane

                  Harness
          state / events / policy
          evidence / permission
                  |
                  v
                 Tools
                  |
                  v
          External Systems
```

Execution results should flow through the Harness before they become an Agent explanation:

```text
Tool
  -> Harness preserves raw execution truth
      -> Agent interprets
          -> Human receives focused view
```

This separation prevents an LLM summary from becoming the only surviving record of reality.

---

# 7. Contract Friction

**Contract friction** is a major motivation and diagnostic concept for Agentification.

External integrations impose several kinds of contracts:

```text
Transport contract
Syntax contract
Schema contract
Protocol contract
Semantic contract
Lifecycle contract
```

The early layers are usually suitable for deterministic software.

Examples:

```text
HTTP framing
JSON parsing
exit codes
SSE framing
schema validation
```

The later layers are where rigid automation becomes expensive:

```text
Did this 200 response actually succeed?
Does this sentence imply expired authentication?
Did this CLI version change its output conventions?
Can this session still be resumed safely?
What should happen after this unexpected partial result?
```

These are examples of **semantic contract friction**.

A preliminary ownership model is:

```text
Transport friction  -> deterministic code / utilities
Schema friction     -> deterministic parser where stable
Semantic friction   -> Agent
Policy boundary     -> Harness
```

This is not yet a complete decision model and remains a major research topic for Palingen.

---

# 8. When Agentification Is Likely Valuable

A project is a strong candidate when it has several of the following characteristics:

- many external systems
- API / CLI / browser interaction mixed together
- unstable or semi-structured output
- frequent interface variation
- large amounts of adapter and parser code
- many semantic branches and fallbacks
- workflows that vary by context
- human operators currently bridge multiple systems manually
- integration cost grows rapidly with each new target

A project may be a poor candidate when:

- inputs are fixed
- outputs are fixed
- sequencing is fixed
- contracts are stable
- behavior is deterministic
- there is little semantic ambiguity

Agentification should absorb **semantic variability and contract friction**, not replace reliable deterministic software for its own sake.

---

# 9. Validation

An Agentified system is not successful merely because an Agent can complete a demo.

At minimum, evaluate:

## Adaptability

How much new code is required to integrate a new system or interface variant?

## Semantic flexibility

Can unfamiliar but understandable outputs be handled without building a new semantic parser immediately?

## Deterministic reliability

Did stable operations remain deterministic instead of being unnecessarily delegated to the model?

## Recoverability

Can execution resume after an Agent crash, human pause, tool failure, or environment interruption?

## Auditability

Can the system answer:

- what capability was invoked?
- with which parameters?
- what raw result was returned?
- what state changed?
- why did the Agent choose the next action?
- where is the original evidence?

## Refactoring value

Did Agentification actually reduce integration friction, semantic glue, and future adaptation cost, or merely replace code with prompts and hidden complexity?

---

# 10. Current Palingen Principles

The following principles are considered stable enough to guide further discussion:

1. **Code provides capabilities, not workflows.**
2. **Agent owns semantic composition.**
3. **Harness owns execution truth.**
4. **LLM is semantic glue, not a replacement for deterministic computation.**
5. **Skills provide strategy and knowledge, not disguised rigid workflows.**
6. **High-level Skills help define the new structure; low-level Skills emerge while dismantling the old one.**
7. **Use nails for structure, glue for semantics, and lubricant for incidental friction.**
8. **Normalize transport, not semantics.**
9. **Preserve raw before interpreting or normalizing it.**
10. **One attention surface, many execution surfaces.**
11. **Concentrate attention, not information.**
12. **Let the Agent compress the view, never the truth.**
13. **Structured truth, flexible language.**
14. **Everything important should be resumable and auditable.**
15. **Rigid where truth matters, fluid where meaning varies.**

---

# 11. Open Questions

These areas are intentionally not finalized yet.

## Agentification decision model

How do we decide, for a specific block of existing code, whether it should become:

- deterministic code
- Tool
- low-level Skill
- high-level Skill
- Agent responsibility
- Harness invariant
- Human task
- removable legacy glue

## Contract-friction model

Can contract friction be measured or classified well enough to predict which interfaces should be Agent-mediated?

## Harness boundary

Exactly which control-flow elements should remain deterministic, and when does a Harness become an overly rigid workflow engine again?

## Skill hierarchy

How should high-level and low-level Skills compose without recreating hidden control flow?

## Agent-generated glue

When may the Agent create temporary parsing or transformation code, and how should repeated glue be promoted into a stable Tool?

## Interaction contract

How much structure should be enforced on Agent-to-human output while preserving natural interaction?

## Validation metrics

Which measurements demonstrate that an Agentification refactor is actually better than the original architecture?

---

# 12. Working Mental Model

The current Palingen mental model can be summarized as:

```text
                           OLD HOUSE
                               |
                         1. UNDERSTAND
                               |
                 +-------------+-------------+
                 |                           |
            2. SEDIMENT                3. DISASSEMBLE
            new structure                 old assets
                 |                           |
      Harness / High Skills       Tools / Low Skills / Reuse
                 |                           |
                 +-------------+-------------+
                               |
                           4. REBUILD
                               |
              Agent + Skills + Harness + Tools
                               |
                           5. VALIDATE
                               |
                       AGENTIFIED SYSTEM
```

The purpose is not to make software less engineered.

It is to move engineering effort to the places where determinism matters, and use Agent intelligence where semantic variability previously forced humans to write and maintain large amounts of brittle glue code.
