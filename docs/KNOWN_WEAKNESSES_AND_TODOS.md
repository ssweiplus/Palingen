# Palingen — Known Weaknesses and TODOs

This document records weaknesses, unresolved assumptions, and follow-up work that remain after the first closed-loop design of the Palingen Agentification Skill.

It is intentionally not a second methodology document. Items belong here when they are not yet proven enough to harden into the core Skill.

---

## 1. Highest-priority validation work

### 1.1 Run Palingen end to end on real projects

The current methodology is internally coherent, but much of it is still design-time reasoning rather than field evidence.

Validate on several materially different project types, preferably including:

- an existing LLM workflow application;
- a human-operated multi-tool workflow with no embedded LLM;
- a mostly deterministic project that Gate 0 should reject;
- a project with valuable intermediate artifacts and recovery needs.

Observe where the Agent:

- gets stuck;
- over-analyzes;
- creates unnecessary artifacts;
- misassigns responsibility;
- over-decomposes stable code;
- recreates workflow logic inside Skills, Tools, or Harness;
- escalates too much to the human;
- fails to preserve operational compatibility.

Do not optimize the methodology further until these failure modes are observed in real use.

---

## 2. Artifact explosion risk

Palingen currently has many possible analysis artifacts:

- project understanding;
- Responsibility Map;
- Harness Mapping;
- Workflow Extraction;
- Glue Map;
- Skill Map;
- Connection Map;
- Slice Plans;
- Validation report;
- optional `.agentification.md`.

The methodology says these are conditional, but an Agent may still generate them mechanically.

### TODO

Validate and likely harden this rule:

> Create a durable artifact only when it carries information that must survive a context boundary, human review boundary, execution boundary, or future reuse boundary.

The **Responsibility Map** should remain the primary living analytical artifact. Other maps should usually be views or optional supporting artifacts rather than mandatory documents.

Need field evidence before deciding whether to encode this rule more strongly in the root Skill.

---

## 3. Root Skill growth risk

The root Skill now contains Gate 0, cross-stage invariants, responsibility principles, execution-truth reminders, Human-role reminders, target-form guidance, and loading instructions.

All of these are useful, but continued growth could make the root Skill duplicate the Stage Skills and references.

### TODO

After real-project trials, reduce the root Skill to only principles whose absence would cause the whole Agentification effort to drift.

Desired long-term shape:

```text
Root Skill = constitution
Stage Skill = current mission
Reference = specialized decision knowledge
```

Do not add new detailed taxonomies to the root Skill by default.

---

## 4. Stage ritualization risk

The five stages are intended as reasoning and context boundaries, not as a rigid project-management workflow.

There is still a risk that an Agent will interpret them as mandatory sequential paperwork:

```text
Understand -> document
Sediment -> document
Disassemble -> document
Rebuild -> document
Validate -> document
```

rather than as adaptive reasoning scopes.

### TODO

During real use, measure whether each stage materially improves decisions.

Watch for:

- artificial waiting for stage completion;
- duplicate analysis across adjacent stages;
- unnecessary human review at stage boundaries;
- failure to revisit Sediment when Disassemble changes assumptions;
- stage documents produced only to satisfy structure.

If observed, simplify stage exit criteria rather than adding more workflow machinery.

---

## 5. Responsibility assignment remains judgment-heavy

The current model uses responsibility atoms plus six dimensions:

- Determinism;
- Semantic Dependency;
- Contract Volatility;
- Truth Criticality;
- Risk / Authority;
- Composability.

This is useful, but there is not yet enough evidence that different Agents will classify ambiguous responsibilities consistently.

### TODO

Collect misclassification examples from real projects, especially:

- Agent vs deterministic policy;
- Tool vs internal Code;
- Skill vs semantic Agent reasoning;
- Harness invariant vs old workflow sequencing;
- Human Judgment vs Agent autonomy;
- deterministic adapter vs semantic glue.

Prefer example-driven calibration over a numeric scoring system.

---

## 6. Skill degeneration risk

A major failure mode is converting workflow code into workflow prose:

```text
workflow.py
   ->
Step 1 / Step 2 / Step 3 in SKILL.md
```

The current `does_not_own` model helps, but has not yet been field-tested.

### TODO

Test whether Skills produced by Palingen actually remain knowledge-bearing rather than sequencing-bearing.

Validate that important Skills can answer:

- What does this Skill teach?
- What decisions remain contextual?
- What does this Skill explicitly not own?
- Which invariants are enforced elsewhere?
- Can the Agent deviate from the suggested strategy when evidence justifies it?

If Skills repeatedly become hidden workflows, strengthen the Skill-layering checks rather than adding more Skill types.

---

## 7. Harness overgrowth risk

Harness has a strong conceptual boundary:

> What must remain correct even if the Agent is wrong?

But real projects may tempt the Agent to move semantic workflow sequencing into Harness under labels such as lifecycle, validation, recovery, or policy.

### TODO

Collect concrete examples where Harness begins to decide business sequencing.

Validate that:

- lifecycle constraints remain mechanical;
- semantic next-action selection remains outside Harness;
- authorization is separated from strategy;
- recovery preserves truth and resumability without reconstructing a fixed business workflow.

---

## 8. Human attention model needs field validation

The current model distinguishes Human roles and intervention modes:

```text
autonomous
reviewable / overrideable
blocking
```

This is conceptually sound, but the correct threshold between reviewable and blocking is still contextual.

### TODO

Evaluate:

- approval fatigue;
- cases where the Agent should have continued autonomously;
- cases where it continued but should have blocked;
- whether questions are asked at the level of human intent rather than implementation detail;
- whether users can naturally inspect, annotate, redirect, branch, and resume.

Do not optimize for minimum human intervention count. Optimize for minimum unnecessary human attention while preserving authority and valuable judgment.

---

## 9. Agentification Slice granularity needs evidence

Agentification Slice is currently the preferred migration unit:

```text
capability
+ semantic decision
+ truth / artifact boundary
```

This appears promising, but there is not yet enough evidence about the right slice size.

### TODO

Observe when slices become:

- too large to expose meaningful semantic decisions;
- too small and create Tool/Skill/interface explosion;
- awkward because old state or artifact contracts cross multiple slices;
- unnecessarily expensive to validate independently.

Retain the coarse-first rule until real evidence suggests more formal guidance.

---

## 10. Target-form assumptions need practical validation

The current target form includes:

- one attention surface, many execution surfaces;
- Agent-owned semantic composition;
- first-class intermediate results;
- progressive disclosure;
- local failure without global workflow failure;
- natural Human intervention.

These are directional properties rather than mandatory architecture components.

### TODO

Validate which of these properties actually produce user value in different project classes.

In particular, avoid forcing a unified interaction surface when a specialized existing UI remains the best place for professional work.

---

## 11. Observability semantics need implementation examples

Palingen deliberately defines meaningful execution-event semantics without mandating JSONL, Event Store, tracing, ELK, database audit, or another backend.

This keeps the method portable, but may leave implementers unsure about the minimum useful event surface.

### TODO

After real implementations, collect a small set of representative patterns for:

- tool invocation / completion;
- authoritative state change;
- artifact availability;
- Human intervention;
- approval change;
- checkpoint / resume / branch;
- local failure / blocked execution.

Keep these as examples, not as a required event schema unless repeated evidence proves a common contract valuable.

---

## 12. Helper tools — useful but not yet designed

Palingen should remain a Skill-first methodology, not become another Agent framework.

Potential deterministic helpers may include:

- repository inventory;
- LLM call-site discovery;
- parser / retry / fallback hotspot discovery;
- call graph generation;
- state-write hotspot discovery;
- artifact/path discovery;
- Human-intervention hotspot discovery;
- dependency and entry-point inspection.

### TODO

Only add helpers that reduce Agent inspection cost without owning semantic decisions or workflow sequencing.

Explicitly avoid drifting toward:

```text
Palingen Runtime
Palingen Workflow Engine
Palingen Agent SDK
```

unless future evidence establishes a real need.

---

## 13. Quantitative scoring remains deferred

Possible future metrics include glue reduction, integration effort, Human attention, resume success, compatibility, semantic error, token cost, and latency.

However, there is currently insufficient evidence for meaningful numeric weights or a universal Agentification score.

### TODO

For now use qualitative judgments plus rationale:

```text
Low / Medium / High
```

Collect comparable observations across several real Agentification projects before considering quantitative scoring.

Do not create numerical precision without empirical grounding.

---

## 14. Existing research backlog needs reconciliation

`docs/RESEARCH.md` predates several settled decisions and still contains older candidate designs such as fixed Event Store / Artifact Store responsibilities and event-sourced execution as a primary research direction.

### TODO

After the first real-project validation pass:

- mark resolved research questions as settled;
- remove or rewrite assumptions superseded by the current Skill;
- move still-open research into this backlog;
- keep historical rationale only where it remains useful.

Do not let outdated research notes silently reintroduce abandoned architecture assumptions.

---

# Current priority

The next major step is **not additional methodology design**.

Priority order:

```text
1. Real-project end-to-end trials
2. Observe failure modes and friction
3. Fix only evidence-backed weaknesses
4. Add small deterministic helper tools where they save real effort
5. Revisit quantitative metrics only after multiple trials
```

The current methodology should be treated as a first design baseline that is ready to be challenged by use.
