# Human Interaction Contract

Use this reference to shape the user experience of a Palingen run from startup through progress, intervention, recovery, and final result presentation.

The interaction surface should reduce human non-goal work while preserving authority and inspectability.

## 1. Startup

Palingen already knows its default objective:

> Agentify the selected target using the Palingen methodology.

Do not ask the user to restate that objective.

Ask only for information that materially changes scope, authority, or optional behavior.

A minimal startup surface may be:

```text
Target
  ./project

Optional
  □ Extract domain semantic seed
     Preserve business concepts and relations for future cross-project alignment / ontology experiments

Optional focus
  [Only when the user wants to emphasize a particular pain point]

[Start Agentification]
```

Do not force the user to choose between internal Palingen stages or to configure an execution workflow.

### Domain semantic seeding

When the experimental semantic-seeding capability is available, offer it as an optional startup choice.

Prefer user-facing language such as:

> Also identify important business concepts, terminology, rules, and relationships so they can be aligned across projects later.

Do not require users to understand OWL, RDF, SHACL, or ontology tooling.

Enabling semantic seeding must not change the primary Agentification objective or block the main run.

## 2. Default execution posture

Prefer:

```text
Autonomous + Reviewable
```

The Agent proceeds on ordinary bounded decisions, while important intermediate conclusions remain inspectable and overrideable.

Block only when human authority, irreversibility, high-impact ambiguity, or human-only information/capability makes intervention necessary.

Do not ask the user to select a process mode merely to expose Palingen's internal methodology.

## 3. Progress presentation

Present execution state, not private reasoning.

A useful progress view answers:

```text
Current stage
Current focus
What has been established
What is active now
Important findings or changed assumptions
Whether human input is needed
Latest durable artifact/checkpoint
Likely next direction
```

Example:

```text
Current stage: Disassemble

Current focus:
Split authentication recovery responsibilities

Established:
✓ login capability remains deterministic
✓ session state is authoritative runtime truth
✓ expiry interpretation is a semantic decision

Active:
→ retry / resume boundary

Waiting for human:
No

Latest durable result:
Responsibility Map updated
```

Avoid pretending semantic work has precise percentage completion.

## 4. Human intervention request

When blocking human help is necessary, ask at the level of intent and consequence rather than low-level implementation detail.

A blocking request should explain:

- why the Agent cannot safely or correctly continue;
- what has already been preserved;
- exactly what the human needs to provide, decide, or perform;
- what will happen after the intervention;
- which alternative controls are available.

Example:

```text
Human help required

Reason:
The target session has expired and the Agent cannot perform the required authentication step.

Already preserved:
- current analysis
- current Responsibility Map
- unfinished slice state

Need from you:
Re-authenticate the target application.

Afterwards:
Tell Palingen the action is complete and it will resume from the current checkpoint.

Other controls:
Pause / Change direction / Skip current slice / Stop
```

Do not reduce human participation to repeated Approve / Reject prompts.

## 5. Human responses are composable

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

## 6. User-initiated control

Where the product surface supports it, keep a small persistent control surface available:

```text
Inspect
Pause
Add note
Redirect
Stop
```

Expose advanced controls progressively when useful:

```text
Branch
Replace result
Skip current slice
Resume
```

The user must be able to intervene even if the Agent has not requested intervention.

## 7. Recovery presentation

When a previous unfinished run is detected, do not replay the entire history.

Present a compact recovery summary:

```text
Unfinished Palingen run detected.

Target:
./project

Current boundary:
authentication recovery

Stage:
Disassemble

Last completed result:
auth capability and truth boundaries established

Paused at:
retry semantics

[Resume] [Inspect] [Change direction] [Abandon]
```

The Agent should recover from durable state/artifacts, not rely on conversation memory alone.

## 8. Result presentation

Use progressive disclosure.

### Level 1 — outcome

Show the acceptance state and major architectural changes.

Example:

```text
Outcome: ACCEPT_WITH_DEFERRED_REFINEMENT

Major responsibility changes:
- authentication interpretation -> Agent
- login execution -> Tool
- session truth -> Harness
- recovery know-how -> Skill

Retained unchanged:
- existing API client
- existing session file contract

Deferred:
- reporting workflow
```

### Level 2 — architecture delta

Show a concise before/after responsibility view rather than a long implementation dump.

### Level 3 — evidence and artifacts

Make detailed artifacts reachable on demand, for example:

- Responsibility Map;
- Harness/Skill/Connection views when they were materially useful;
- Slice Plan / implementation evidence;
- Validation evidence;
- Domain Semantic Seed when enabled;
- raw evidence needed for audit or debugging.

> Compress the presentation, never the truth.

## 9. Interaction anti-patterns

Avoid:

- asking the user to redefine Palingen's own goal;
- exposing internal stage sequencing as configuration burden;
- frequent low-value approval prompts;
- vague requests such as "please handle this manually" without saying what and why;
- hiding partial success behind a global FAILED state;
- displaying private reasoning instead of observable progress;
- dumping every artifact onto the primary attention surface;
- forcing ontology terminology on users who only asked for Agentification.

## Principle

> Ask only for information or authority that materially changes what Palingen can safely and correctly do.
