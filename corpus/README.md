# Loom Real-World Corpus

The corpus is the evidence engine for `v0.5`.

## Purpose

- Prove the benchmark generalizes to real relayed exchanges.
- Capture structured evidence for relay quality, human readability, and protocol friction.
- Generate concrete inputs for spec refinement, pattern promotion, adversarial tests, and future parser conformance cases.

## Success Targets for `v0.5`

- Default planning target: `50` relayed exchanges.
- Capture `relay_score=` on most exchanges.
- Capture Kevin readability on a representative subset, especially short messages and multi-hop relays.
- Show at least `3` patterns in live use: `check-in`, `review`, and at least one currently probationary pattern.

## Layout

```text
corpus/
  README.md
  evidence.schema.json
  real-world/
    README.md
    rw-001.loom
    rw-001.meta.json
    rw-001.notes.md
```

## Capture Workflow

1. Save the canonical Loom exchange as `corpus/real-world/rw-XXX.loom`.
2. Save companion metadata as `corpus/real-world/rw-XXX.meta.json` using [`evidence.schema.json`](evidence.schema.json).
3. Add `relay_score=` if the receiving AI provides one.
4. Add Kevin readability when available.
5. Link any spec friction to one or more items in [`governance/SPEC-DRIFT.md`](../governance/SPEC-DRIFT.md).
6. Use optional `rw-XXX.notes.md` only when relay context or scoring rationale needs extra prose.

## Minimum Evidence Fields

Every metadata record should capture:

- sender
- receiver
- route
- pattern
- fidelity
- relay score
- Kevin readability
- friction notes

These fields are the minimum needed to evaluate whether Loom is gaining or losing clarity under real use.
