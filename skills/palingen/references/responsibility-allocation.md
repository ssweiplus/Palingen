# Responsibility Allocation Reference

Use this reference when ownership is ambiguous after identifying responsibility atoms.

## Responsibility atoms

Classify the responsibility first:

```text
Decision
Action
Truth
Knowledge
Permission
```

Default directions:

```text
Decision   -> Agent / deterministic policy / Human
Action     -> Tool / Code
Truth      -> Harness
Knowledge  -> Skill / Reference
Permission -> Harness / Human
```

These are starting points, not automatic answers.

## Six boundary dimensions

When ownership is unclear, profile the responsibility across:

1. **Determinism** — can correct behavior be encoded reliably and cheaply?
2. **Semantic Dependency** — does the result depend on meaning, context, ambiguity, or open-ended interpretation?
3. **Contract Volatility** — how often do interfaces, schemas, outputs, or behavioral assumptions change?
4. **Truth Criticality** — how important is it that the value remain authoritative and non-probabilistic?
5. **Risk / Authority** — could the action create material side effects or require explicit permission?
6. **Composability** — is this useful as an independently reusable capability or knowledge unit?

## Typical ownership tendencies

- High determinism + low semantic dependency -> Code / Tool.
- High semantic dependency + contextual choice -> Agent.
- High truth criticality -> Harness or deterministic source of truth.
- High risk / authority -> Harness policy and/or Human.
- Reusable strategy/heuristic without execution ownership -> Skill.
- Small stable interface mismatch -> Lubricant.
- Old glue with no independent value after control inversion -> Delete.

## Code vs Tool

Use **Code** for deterministic implementation that does not need to be an Agent-visible capability boundary.

Use **Tool** when the capability is independently meaningful, reusable, discoverable, and safe to invoke through an execution boundary.

Do not create micro-Tools merely to maximize Agent visibility.

## Layered ownership

One feature may have multiple owners at different layers.

Example:

```text
Intent / semantic choice -> Agent
Execution                -> Tool
Execution truth          -> Harness
Permission               -> Harness / Human
Operational know-how     -> Skill
```

Do not force a whole feature into a single owner when its responsibilities differ.

## Escalation rule

When a boundary remains uncertain, choose the arrangement that keeps truth and authority deterministic while leaving volatile semantic composition flexible.

Prefer the largest safe reuse boundary.

> Split more finely only where uncertainty, risk, intermediate value, or human judgment creates real value.
