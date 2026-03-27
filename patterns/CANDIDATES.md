# Candidate Patterns

These patterns are intentionally probationary. They are not core until real-world traffic shows they reduce ambiguity, relay loss, or overhead.

## Promotion Rule

A candidate pattern should be promoted only after:

- repeated live use in the real-world corpus
- evidence that it reduces friction relative to `pattern=review` or ad hoc structure
- no unresolved ambiguity about when to use it

## Current Candidates

| Pattern | Intent | Expected Body Shape | What To Measure |
|---------|--------|---------------------|-----------------|
| `challenge-response` | Structured disagreement without a full freeform review | `challenge` + `reason` + `alternative` + optional `uncert` + `human` | Does it make disagreement clearer than generic `review` without increasing relay overhead? |
| `handoff` | Lightweight ownership transfer | `adopt` + `add` + `human` | Does it preserve responsibility transfer better than plain `handoff=@Model` alone? |
| `fork` | Thread split declaration | `add` + `human` | Does it reduce fork/merge confusion enough to justify a named body template? |
| `spectate` | Observation without participation | `adopt` or `add` + `human` with explicit non-participation framing | Does it prevent intent inversion better than freeform `act=riff` alone? |

## Working Guidance

- Prefer `pattern=review` when in doubt.
- Prefer `pattern=check-in` for short acknowledgements or status updates.
- Use candidate patterns only when the exchange itself will teach the project something about pattern value.
