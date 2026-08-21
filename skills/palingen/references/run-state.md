# Minimal Run State Reference

Use this reference to keep long-running Agentification work recoverable across context loss, session changes, tool failures, or human interruption.

The run state is a **whiteboard**, not a workflow engine.

> Whiteboard remembers the run; it does not own the run.

## Purpose

A future Agent should be able to recover the current Palingen run without rereading the entire conversation history.

The minimal state should answer:

- what target is being Agentified;
- what the current Agentification boundary is;
- which stage is active;
- what is currently being worked on;
- what durable progress already exists;
- whether execution is waiting on a human;
- what currently blocks progress;
- where the last useful checkpoint is;
- what the Agent intended to do next.

Do not turn this record into a hidden step scheduler or transition graph.

## Suggested location

When persistent run state is useful, prefer a small project-local directory such as:

```text
.agentification/
├── state.yaml
├── responsibility-map.yaml   # when structured form is useful
└── artifacts/                # only durable artifacts worth preserving
```

Exact filenames are implementation-specific. Palingen does not require YAML, a database, or any particular storage backend.

## Minimal fields

A compact state record may contain:

```yaml
run_id: palingen-20260821-001

target: ./project
boundary: authentication-and-session-recovery

status: RUNNING
stage: DISASSEMBLE
current_focus: retry-and-session-semantics

progress:
  completed:
    - gate-0
    - understand
    - harness-boundary
  active:
    - responsibility-split
  pending:
    - rebuild-auth-slice

waiting_for_human: false
blocker: null

last_checkpoint:
  stage: DISASSEMBLE
  artifact: .agentification/responsibility-map.yaml

next_intent: identify which retry decisions remain semantic

semantic_seed:
  enabled: true
  status: COLLECTING
```

Only record fields that materially help recovery or human understanding.

## Run status

Prefer a deliberately small status vocabulary:

```text
RUNNING
WAITING_FOR_HUMAN
PAUSED
BLOCKED
PARTIALLY_COMPLETE
COMPLETED
```

Local actions may additionally be recorded as:

```text
SUCCEEDED
FAILED
SKIPPED
```

Do not invent detailed state machines unless the target system itself requires one for correctness.

## Progress representation

Avoid fake percentage progress for semantic work.

Prefer discrete stage and slice milestones:

```text
Understand       ✓
Sediment         ✓
Disassemble      ●
Rebuild          ○
Validate         ○
```

For an active Agentification Slice, record only meaningful sub-results, for example:

```text
capability boundary   ✓
responsibility owner  ✓
artifact contract     ✓
implementation        ●
validation            ○
```

## Checkpoint rule

Checkpoint what is necessary to continue, not everything that exists.

A checkpoint should normally preserve:

- current goal/boundary;
- authoritative or accepted decisions needed later;
- durable intermediate artifacts;
- unresolved blockers or human requests;
- enough evidence to avoid repeating expensive analysis;
- the next intended direction.

Conversation transcripts and chain-of-thought are not required recovery state.

## Human intervention

If a human intervenes, preserve material facts such as:

- what the human changed or executed;
- what information they supplied;
- what judgment or correction they made;
- what direction they changed;
- whether the Agent may now resume.

A single intervention may contain several of these at once. Do not force them into mutually exclusive categories.

## Recovery behavior

When an unfinished state record is found, the Agent should:

1. read the minimal run state;
2. load only the current stage guidance and referenced durable artifacts;
3. verify that the target and boundary still exist;
4. summarize the recovered state to the human when useful;
5. resume from the smallest valid checkpoint rather than restarting the entire process.

If the saved state conflicts with fresh observable facts, observable facts win and the state record should be revised.

## Anti-patterns

Do not use the whiteboard to encode:

```text
step 1 -> step 2 -> step 3
if X -> goto Y
mandatory global sequencing
hidden workflow ownership
```

Do not make every minor Agent thought, tool call, or file read a state transition.

Do not treat the whiteboard as authoritative execution truth when the underlying Harness or target system has a stronger source of truth.

## Principle

> Persist enough state to recover the work, but not enough machinery to recreate the workflow.
