# Minimal Run State Reference

Use this reference only when an Agentification run is long enough that context loss, session changes, human interruption, or tool failure could make recovery expensive.

The run state is a **whiteboard**, not a workflow engine.

> Whiteboard remembers the run; it does not own the run.

## Recovery question

A new Agent should be able to answer, without rereading the whole conversation:

```text
What target am I working on?
What boundary is currently being Agentified?
Which reasoning scope is active?
What accepted progress must not be lost?
What is blocking or waiting on a human?
Where is the last useful checkpoint?
What was the intended next direction?
```

If the work is short and easy to reconstruct, do not create persistent run state.

## Minimal record

Use the project's simplest convenient representation. YAML is only an example.

```yaml
run_id: palingen-20260821-001
target: ./project
boundary: authentication-and-session-recovery

status: RUNNING
stage: DISASSEMBLE
current_focus: retry-and-session-semantics

accepted_progress:
  - login remains a deterministic capability
  - session state is authoritative runtime truth

waiting_for_human: false
blocker: null

last_checkpoint:
  artifact: .agentification/responsibility-map.yaml

next_intent: determine whether retry choice is semantic or invariant

semantic_seed_enabled: true
```

Only record fields that materially improve recovery or human understanding.

## Status vocabulary

Prefer a very small vocabulary:

```text
RUNNING
WAITING_FOR_HUMAN
PAUSED
BLOCKED
PARTIALLY_COMPLETE
COMPLETED
```

Do not model every tool call or internal thought as a state transition.

## Progress presentation

Avoid fake percentages.

Use coarse milestones only when they help orientation:

```text
Understand       ✓
Sediment         ✓
Disassemble      ●
Rebuild          ○
Validate         ○
```

The whiteboard does not need a full pending-task list. `current_focus`, accepted progress, blocker, checkpoint, and `next_intent` are normally enough.

## Checkpoint rule

> Checkpoint what is necessary to continue, not everything that exists.

Preserve only information that prevents expensive or unsafe reconstruction, such as:

- accepted responsibility/boundary decisions;
- durable intermediate artifacts with future value;
- unresolved blockers or human requests;
- evidence needed to avoid repeating important analysis;
- the current intended direction.

Conversation transcripts and private reasoning are not recovery state.

## Human intervention

A human response may contain several things at once:

```text
action performed
new information
correction
annotation
authority decision
change of direction
```

Preserve the material facts together rather than forcing mutually exclusive response types.

## Recovery behavior

When an unfinished record is found:

1. read the minimal state;
2. load the active Stage Skill and only referenced durable artifacts;
3. verify the target/boundary against fresh observable facts;
4. revise stale state when evidence conflicts with it;
5. resume from the smallest valid checkpoint.

The run-state record is not authoritative when the target system or Harness has a stronger source of truth.

## Do not encode

```text
step 1 -> step 2 -> step 3
if X -> goto Y
mandatory global sequencing
per-tool transition graphs
hidden business workflow
```

Do not create a database, event store, task manager, or dedicated runtime merely to implement this reference unless the target project independently needs one.

## Principle

> Persist enough state to recover the work, but not enough machinery to recreate the workflow.
