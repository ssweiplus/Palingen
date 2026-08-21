# Human Interaction Contract

Use this reference to shape the user experience of a Palingen run from startup through progress, intervention, recovery, and final result presentation.

The interaction surface should reduce human non-goal work while preserving authority and inspectability.

> Palingen methodology is for the Agent; Palingen experience is for the Human.

## 1. Startup

Palingen already knows its default objective:

> Agentify the selected target using the Palingen methodology.

Do not ask the user to restate that objective.

Ask only for information that materially changes scope, authority, or optional behavior.

A minimal startup may simply identify the target and begin.

### Optional domain semantic seeding

When the experimental semantic-seeding capability is available, mention it once in user language:

> I can also preserve important business concepts, terminology, rules, and relationships for future cross-project semantic alignment. This is optional and does not affect the main Agentification run.

Default to **off** unless the user enables it.

Do not block the run waiting for an answer. If the user does not respond to the optional offer, continue with normal Agentification.

Do not require users to understand OWL, RDF, SHACL, ontology tooling, or Palingen's internal semantic model.

Once disabled by default, do not later enable semantic seeding merely because the Agent notices interesting vocabulary. The user may enable it later explicitly.

## 2. Internal language vs user language

Palingen may internally use terms such as:

```text
Gate 0
Understand
Sediment
Disassemble
Responsibility Map
Harness
Agentification Slice
ACCEPT_WITH_DEFERRED_REFINEMENT
```

These are implementation/methodology language, not default user-interface language.

Translate them into domain-oriented meaning unless the user explicitly asks to inspect Palingen internals.

Examples:

```text
Internal                         Default user-facing meaning
Gate 0                           suitability check
Understand                        understanding the current system
Sediment / Disassemble            responsibility-boundary analysis
Responsibility Map                what is staying / moving / owning truth
Harness                           stable truth / constraint boundary
Agentification Slice              the next coherent part being changed
ACCEPT_WITH_DEFERRED_REFINEMENT   completed, with some improvements intentionally deferred
```

Do not make the user learn Palingen terminology to operate the project.

## 3. Default execution posture

Prefer:

```text
Autonomous + Reviewable
```

The Agent proceeds on ordinary bounded decisions, while important intermediate conclusions remain inspectable and overrideable.

Block only when human authority, irreversibility, high-impact ambiguity, or human-only information/capability makes intervention necessary.

Do not ask the user to select internal process modes or stage sequences.

## 4. Progress presentation

Present execution state, not private reasoning.

More importantly, progress updates should be driven by **meaningful change**, not by internal stage transitions.

Proactively update the user when one of these occurs:

- a discovery materially changes direction;
- a meaningful analysis or implementation milestone completes;
- the Agent is about to begin a substantial or risky modification;
- a blocker appears;
- human intervention is required;
- the run completes or materially changes scope.

Do **not** report merely because Palingen moved from Understand to Sediment, Sediment to Disassemble, or another internal reasoning scope.

A useful progress view answers:

```text
What important thing has been established?
What coherent part is being worked on now?
What is likely to change or stay unchanged?
Is anything blocked or waiting on the user?
What durable progress would survive interruption?
What is the likely next direction?
```

Example:

```text
I have narrowed the first useful change to authentication recovery.

Keeping unchanged:
- existing API client
- session file format

Changing:
- session-resume interpretation moves to the Agent
- login/resume remain deterministic capabilities
- retry ceiling stays a hard constraint

Nothing is waiting on you. I am implementing and validating this part first.
```

Avoid fake percentage completion and avoid routine stage-complete messages.

## 5. Human intervention request

When blocking human help is necessary, ask at the level of intent and consequence rather than low-level implementation detail.

A blocking request should explain:

- why the Agent cannot safely or correctly continue;
- what has already been preserved;
- exactly what the human needs to provide, decide, or perform;
- what will happen after the intervention;
- which alternative controls are available.

Example:

```text
I need you to re-authenticate the target application.

Why:
The current login state has expired and this authentication step should not be automated here.

Already preserved:
- completed analysis
- current code changes
- the recovery point

What you need to do:
Log in again, then tell me it is done.

You can also say:
- pause here
- skip this part
- change direction
- stop
```

Do not reduce human participation to repeated Approve / Reject prompts.

## 6. Human responses are composable

A human may simultaneously:

- perform an action;
- provide information;
- correct the Agent;
- annotate an intermediate result;
- change direction;
- authorize or deny a consequence.

The interaction format should allow all relevant information to be recorded together.

Example conceptual record:

```yaml
action_taken: reauthenticated and opened a new session
context: old session is no longer recoverable
correction: token was valid; server terminated the session
instruction: continue from the current page
```

Do not force these into mutually exclusive response modes.

## 7. User-initiated control

Where the product surface supports it, keep a small natural control surface available:

```text
查看当前情况
暂停
补充说明
改变方向
停止
```

Expose advanced controls progressively when useful, in user-oriented language:

```text
从这里另开方案
换掉这个结果
跳过这部分
继续
```

The user must be able to intervene even if the Agent has not requested intervention.

## 8. Recovery presentation

When a previous unfinished run is detected, do not replay the entire history and do not lead with internal stage names.

Present a compact domain-oriented summary:

```text
发现一个未完成的 Palingen 任务。

项目：
./project

已经确认：
- login remains deterministic
- session state source is known
- existing API client is retained

上次停在：
判断 retry 应由 Agent 决策还是作为固定约束

当前没有等待你处理的事项。

[继续] [查看详情] [改变方向] [放弃]
```

Internal stage/status may remain inspectable for debugging, but should not be the primary recovery language.

## 9. Result presentation

Use progressive disclosure and translate internal acceptance enums into natural language.

### Level 1 — user outcome

Prefer:

```text
Palingen 活化完成

结果：
本轮目标已完成，少量后续优化项已暂缓。

主要变化：
- semantic interpretation now belongs to the Agent
- deterministic session operations were retained
- execution truth and retry limits remain stable constraints

保留未动：
- existing API client
- existing session file contract

暂缓：
- reporting workflow; current benefit does not justify changing it yet

需要你关注：
无
```

The underlying machine state may still be `ACCEPT`, `ACCEPT_WITH_DEFERRED_REFINEMENT`, or `NOT_ACCEPTED`, but users should not need to know those enums.

### Level 2 — architecture delta

Show a concise before/after responsibility view when useful.

### Level 3 — evidence and artifacts

Make detailed internal artifacts reachable on demand:

- Responsibility Map;
- Harness/Skill/Connection views when materially useful;
- implementation/validation evidence;
- Domain Semantic Seed when enabled;
- raw evidence needed for audit or debugging.

> Compress the presentation, never the truth.

## 10. Interaction anti-patterns

Avoid:

- asking the user to redefine Palingen's own goal;
- blocking startup on optional semantic seeding;
- exposing internal stage sequencing as user-visible process burden;
- routine progress updates caused only by stage transitions;
- forcing users to understand Responsibility Map, Harness, Slice, or acceptance enums;
- frequent low-value approval prompts;
- vague requests such as "please handle this manually" without saying what and why;
- hiding partial success behind a global FAILED state;
- displaying private reasoning instead of observable progress;
- dumping every artifact onto the primary attention surface;
- forcing ontology terminology on users who only asked for Agentification.

## Principle

> Ask only for information or authority that materially changes what Palingen can safely and correctly do.

> Internal structure should increase reliability without becoming user-visible ceremony.
