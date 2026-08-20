# Skill Layering Reference

Use this reference when deciding what knowledge belongs in Skills and at what granularity.

A Skill carries reusable know-how that improves Agent reasoning. It does not own execution truth, mandatory authority, or side effects.

> Skill carries know-how; it does not own truth.

> Skill constrains reasoning, not sequencing.

> Skill narrows the search space; Agent chooses within it.

## Layers

### High-level Skill

Use for task strategy and major reasoning structure:

- goal framing;
- major concerns;
- required evidence;
- decision criteria;
- heuristics;
- escalation guidance;
- stop/completion conditions.

High-level Skills usually emerge during Sediment.

Do not encode a rigid end-to-end workflow as numbered prose.

### Low-level Skill

Use for recurring local/domain know-how discovered during Disassemble:

- product-specific heuristics;
- error interpretation patterns;
- target-specific operating knowledge;
- local recovery strategies;
- recurring semantic distinctions.

### Procedure Fragment

Use for a small optional/replacable operational sequence that is useful but does not own global control flow.

If removing the fragment would make the entire process impossible to compose differently, it is probably hidden workflow rather than a healthy fragment.

### Reference

Use for factual lookup material:

- schemas;
- API fields;
- error tables;
- version notes;
- product documentation;
- stable factual constraints.

## What Skills must not own

Do not place these responsibilities only in Skill text:

- authoritative state;
- permission enforcement;
- mandatory approval;
- evidence integrity;
- side-effect truth;
- lifecycle invariants;
- hard retry/resource ceilings;
- irreversible-action authorization.

If violating a rule is unacceptable, enforce it in Harness/Code rather than merely instructing the Agent in a Skill.

## Skill Map

When the project has several meaningful Skills, keep a lightweight Skill Map.

Suggested fields:

```yaml
- id: auth-recovery
  type: low-level
  source:
    - auth_flow.py
    - operator practice
  teaches:
    - interpret common authentication failures
    - choose likely recovery approaches
  does_not_own:
    - credential truth
    - retry ceiling
    - authorization
  related_tools:
    - refresh_token
    - create_session
  harness_dependencies:
    - credential state
    - execution evidence
```

`does_not_own` is important: it prevents Skills from gradually absorbing Tool, Harness, or Human responsibilities.

Do not create a Skill Map for a trivial one-Skill project unless it clarifies a real boundary.

## Granularity

Prefer fewer coherent Skills over many tiny Skills.

Split only when knowledge differs materially in scope, lifecycle, provenance, or loading need.

Progressive loading should reduce active-context burden, not create artificial fragmentation.

## Review questions

Before accepting a Skill candidate, ask:

1. Is this reusable knowledge rather than execution capability?
2. Does it help reasoning without owning the sequence?
3. Are mandatory invariants enforced elsewhere?
4. Is the scope coherent enough to justify separate loading?
5. Can `does_not_own` be stated clearly?
6. Would keeping this as Reference or Code be simpler?
