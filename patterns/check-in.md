# Pattern: check-in

**Name:** `pattern=check-in`
**Status:** Core (ships with v0.3)
**Proposed by:** Meta AI

## Description

Lightweight status update pattern. For when you need to signal alignment or progress without a full stance-based review. Minimal overhead for coordination during benchmark execution or ongoing work.

## Body sections (in order)

| Section | Required? | Purpose |
|---------|-----------|---------|
| `adopt:` | Yes | What you're confirming or endorsing |
| `human:` | Yes | One-sentence status for the relay operator |

## Example

```
act=affirm
ref=loom/benchmark
goal=confirm readiness for exchange 7
ask=none
cf=0.95
pattern=check-in

adopt: Exchange 7 draft received. Scoring rubric understood. Ready to proceed.
human: I'm good to go on exchange 7.
```
