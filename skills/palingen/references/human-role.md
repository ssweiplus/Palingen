# Human Role Reference

Use this reference when deciding where and how humans participate in Agentified execution.

Human participation should preserve authority and judgment without turning the user into an approval machine.

## Human roles

A human may act as:

- **Authority** — grants permission for risky, irreversible, scope-changing, or otherwise protected actions.
- **Judgment** — resolves meaningful ambiguity, probability, or value questions where human context matters.
- **Provider** — supplies credentials, external facts, or human-only information.
- **Executor** — performs an environment action that the Agent cannot or should not perform directly.
- **Annotator** — corrects, enriches, labels, or explains intermediate results.
- **Controller** — inspects, pauses, branches, skips, redirects, replaces, or resumes execution.

A single situation may involve more than one role.

## When to escalate

Escalate because of one or more of:

- authority belongs to the human;
- the action is materially irreversible;
- evidence is insufficient and the consequence is important;
- required information or capability is human-only.

Uncertainty alone does not require a human decision.

> Human escalation is not a substitute for Agent reasoning.

## Intervention modes

Use the least intrusive mode that preserves value and authority.

### Autonomous

Agent proceeds without interruption when consequences are bounded, recoverable, and reasonably supported by evidence.

### Reviewable / Overrideable

Agent proceeds with a visible decision or intermediate result that the human may inspect or override without blocking normal progress.

This should be the preferred mode for many uncertain but low-risk judgments.

### Blocking

Require explicit human input only when authority, irreversibility, high-impact ambiguity, or human-only information makes it necessary.

## Interaction quality

Ask at the level of human intent and consequence, not low-level implementation detail.

Prefer one meaningful authorization over many per-call confirmations.

Do not ask the user to resolve uncertainty that the Agent can reasonably handle with bounded downside and recovery.

Concentrate human attention where uncertainty, impact, and irreversibility intersect.

## User-initiated intervention

Humans must be able to intervene even when the Agent has not requested it, where the product surface allows:

```text
inspect
pause
annotate
replace
branch
skip
redirect
resume
```

Material human actions should become observable execution facts/events.

## Lightweight Human Role Map

When useful, record:

```yaml
situation: production write
role: Authority
mode: blocking
reason: irreversible/high-impact side effect
default: deny until approved
override_allowed: true
```

Do not create a Human Role Map when the project has no meaningful intervention decisions.

## Principle

> Maximize useful autonomy while minimizing unnecessary human interruption.
