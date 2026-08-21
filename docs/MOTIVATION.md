# Why Palingen Exists

Palingen did not begin from the desire to build another general-purpose Agent framework. Its starting point is narrower and practical: existing tools and workflow-oriented AI applications often impose too much integration work, interface switching, and opaque automation on the user.

## 1. Attention fragmentation

Open-source tools expose different interaction surfaces: CLI, Web UI, configuration files, notebooks, dashboards, browser extensions, API consoles, and custom result views.

When several tools must be used together, the human becomes the real orchestrator:

```text
Tool A UI
   -> Tool B CLI
      -> Tool C config
         -> inspect logs
            -> copy output
               -> Tool D UI
```

The user's attention is repeatedly transferred from the actual task to the mechanics of operating each tool.

Palingen therefore adopts:

> **One attention surface, many execution surfaces.**

The preferred user experience is a concentrated CLI, chat, IDE, or TUI surface. The Agent mediates the semantic interaction while heterogeneous tools remain execution backends.

This is **attention consolidation**, not information deletion.

> **Concentrate attention, not information.**

## 2. Integration burden, especially around LLMs

Workflow-oriented AI software commonly asks the application developer or operator to integrate the LLM explicitly:

```text
application
  -> configure provider
  -> configure endpoint
  -> define request contract
  -> handle streaming
  -> parse response format
  -> repair malformed structured output
  -> normalize provider differences
  -> connect the next workflow step
```

This reverses the advantage of using an LLM: a highly capable semantic system is wrapped in deterministic glue so that fixed workflow code can understand it.

Palingen explores the opposite control relationship:

```text
Traditional:
Application -> integrates LLM

Agentified:
Agent -> integrates applications
```

The Agent runtime already possesses the LLM and the ability to interpret text, JSON, CLI output, files, and irregular results. Existing projects can therefore expose capabilities instead of each project implementing its own LLM contract and orchestration layer.

## 3. Opaque automation

Many fixed workflows hide the process and expose only the final status:

```text
Input
  -> opaque workflow
      -> SUCCESS / FAILURE / ERROR
```

This is unacceptable for long-running or exploratory work when useful intermediate results may already exist.

A failure late in the workflow should not erase the value of earlier steps.

> **A failed step should not become a failed workflow.**

An Agentified system should preserve useful execution facts and intermediate results as inspectable units:

```text
Run
├── Action A
│   ├── input
│   ├── raw output
│   └── success
├── Action B
│   ├── artifact
│   └── success
└── Action C
    ├── error
    ├── evidence
    └── failed
```

The human should be able to:

- inspect;
- interrupt;
- edit or annotate;
- retry where appropriate;
- branch;
- reuse intermediate artifacts;
- replace one capability;
- resume from a checkpoint.

## 4. Automation should not remove process ownership

Traditional automation often creates this ownership model:

```text
Software owns the process.
Human owns the initial input and final output.
```

Palingen prefers:

```text
Agent helps advance the process.
Harness preserves execution truth, constraints, and recovery anchors.
Human retains ownership of goals and important consequences.
```

The system may automate execution without taking away the user's ability to understand and intervene.

> **Automate execution, not process ownership.**

This is particularly important when an operation is exploratory, expensive, long-running, uncertain, or partially recoverable.

## 5. Granular failure and recoverable work

An Agentified application should make failure local whenever possible.

Instead of:

```text
workflow = ERROR
```

prefer:

```text
A = complete
B = complete
C = failed
checkpoint = B
artifacts = preserved
next options = retry / modify / branch / stop
```

This motivates deterministic support for whichever execution facts are actually needed, such as:

- authoritative state relevant to continuation;
- meaningful execution observations;
- useful intermediate artifacts;
- raw evidence;
- minimal checkpoints;
- human intervention facts.

Palingen does not require these to live in one event store, database, file format, or runtime. The point is that probabilistic orchestration must not make execution truth disposable.

## 6. Four practical liberations

The original motivation can be summarized as four forms of liberation.

### Attention liberation

Reduce UI and tool-switching burden by concentrating human interaction around one semantic surface.

### Integration liberation

Reduce the amount of LLM-provider, parser, adapter, and workflow glue that each application must implement independently.

### Workflow liberation

Turn capabilities that were previously locked into one rigid sequence into composable actions that an Agent can select contextually.

### Process liberation

Make intermediate state, evidence, artifacts, failures, and intervention points available to the human instead of burying them inside an opaque workflow.

## 7. The intended experience

The goal is not merely software that can act autonomously.

It is software that is easier to use, combine, inspect, interrupt, repair, and resume.

```text
                 Heterogeneous tools
          API / CLI / Browser / AI apps
                    |       |
                    +---+---+
                        |
                contract friction
                UI fragmentation
                workflow rigidity
                 opaque failures
                        |
                        v
                 Agentification
                        |
          +-------------+-------------+
          |             |             |
      Attention      Semantic      Process
     consolidation   integration    ownership
          |             |             |
          +-------------+-------------+
                        |
                 Agent Surface
                        |
                     Harness
                        |
               granular capabilities
```

Palingen should remain grounded in this motivation as its methodology evolves. The purpose is not to maximize autonomy. The purpose is to make heterogeneous software more naturally operable and composable by humans through an Agent, without sacrificing execution truth or control of the process.
