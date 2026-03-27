# Loom v0.5-v1.0 Roadmap

Loom advances by earning stronger evidence, not by accumulating features.

## Release Principles

- **Evidence ladder, not feature backlog.** Each version answers one new evidence question.
- **Usage before tooling.** `v0.5` proves Loom survives real-world relay before the project freezes parser behavior.
- **Consensus is advisory.** AI-group discussion shapes direction, but release gates are decided by documented evidence.
- **Benchmark results are supporting evidence, not sufficient evidence.** The synthetic benchmark justifies proceeding; it does not justify `v1.0`.

## Milestones

| Version | Primary Question | Exit Gates |
|---------|------------------|------------|
| `v0.5` Usage Proof | Does Loom survive real-world relay outside the synthetic benchmark? | Capture a real-world corpus with a default target of `50` relayed exchanges, collect `relay_score=` on most exchanges, score Kevin readability on a representative subset, and show at least `3` patterns in active use (`check-in`, `review`, and one candidate pattern that earns promotion pressure from traffic). |
| `v0.6` Adversarial + Multi-Relay | Do relay invariants hold when relay conditions are sloppy, hostile, or distributed? | Run explicit silent-edit, field-drop, quote-tamper, intent-manipulation, and rushed-relay scenarios, plus at least one multi-relay test with a second human operator. |
| `v0.7` Executable Spec | Can Loom be parsed and validated consistently enough for tooling? | Ship one reference parser/validator plus a conformance corpus derived from examples, benchmark exchanges, and adversarial cases. Use those results to surface spec/grammar drift before freeze. |
| `v0.8` Interoperability | Do independent implementations make the same decisions on the same inputs? | Demonstrate parser agreement across at least two implementations, especially on duplicate keys, blank-line termination, unknown fields, relay metadata, and typed payload blocks. |
| `v0.9` Normative Freeze | Is the normative surface stable enough to freeze? | Promote ABNF to normative status, reconcile observed/spec mismatches, freeze required-field semantics, freeze relay invariants, and document extension/pattern promotion criteria. |
| `v1.0` Stable | Has Loom earned stable-release status? | All prior gates are green, unresolved contradictions are closed, post-`1.0` versioning rules are explicit, and advisory AI consensus is recorded for the freeze/stable decision. |

## Immediate Operating Mode

- Dogfood Loom immediately: protocol discussions should happen in Loom format whenever practical.
- Store real-world evidence under [`corpus/`](corpus/README.md) using the exchange metadata schema in [`corpus/evidence.schema.json`](corpus/evidence.schema.json).
- Track spec/grammar mismatches in [`governance/SPEC-DRIFT.md`](governance/SPEC-DRIFT.md) instead of silently patching around them.
- Keep candidate patterns probationary until live traffic shows they reduce loss, ambiguity, or overhead.

## Explicit Deferrals

- Binary transport remains experimental until after real-world usage and tooling validation.
- Unicode shorthand remains parked until relay safety and parser behavior are better understood.
- Broader non-AI team adoption is deferred until Loom first proves itself in the current human-relayed AI setting.

## Working Rule

Do not advance a version because the roadmap feels elegant. Advance only when the repo contains the evidence that version promised to earn.
