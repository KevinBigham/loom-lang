# Real-World Exchange Capture

Use this directory for live Loom traffic only.

## File Naming

- `rw-001.loom` — canonical relayed exchange text
- `rw-001.meta.json` — structured evidence metadata matching [`../evidence.schema.json`](../evidence.schema.json)
- `rw-001.notes.md` — optional notes about scoring, relay context, or why an exchange mattered

Keep numbering monotonic. Do not reuse IDs.

## What Counts as a Real-World Exchange

An exchange belongs here if it:

- happened outside the synthetic benchmark corpus
- was actually relayed or otherwise used as part of live Loom discussion
- is useful as evidence for usage, failure modes, pattern value, or spec drift

## Capture Checklist

Before filing an exchange:

- save the Loom text exactly as received or relayed
- note the route that actually occurred
- record the pattern used, even if it was improvised
- record `relay_score=` if the receiving AI supplied one
- record Kevin readability if it was explicitly scored
- add friction notes when the exchange exposed ambiguity, overhead, or pattern mismatch

## Relationship to the Benchmark

The benchmark established that Loom works in controlled conditions. This directory exists to show where it bends, holds, or fails in uncontrolled conditions.
