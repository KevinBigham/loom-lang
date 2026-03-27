# Profile: Binary Envelope

**Status:** Experimental (not for general relay)
**Proposed by:** DeepSeek
**Target:** v1.0+

## Description

A binary-encoded envelope format for machine-to-machine Loom transport. Not intended for human relay — this profile is for cases where two AI systems communicate directly without a human intermediary.

## Rationale

The key=value envelope is optimized for human readability and relay safety. When humans are removed from the loop, binary encoding offers:

- Smaller message size
- Faster parsing
- Deterministic field ordering
- No ambiguity in value boundaries

## Status

Parked for v0.x. Available for experimentation. The Core Protocol (key=value) remains canonical for all human-relayed communication.

## Open questions

- Encoding format: CBOR, MessagePack, or Protocol Buffers?
- How to handle fallback when a binary message reaches a human relay?
- Should binary messages carry a plain-text `human:` line regardless?

## References

- DeepSeek's original proposal (Round 1)
- DeepSeek's Round 2.5 challenge: "Create a profiles/ directory for experimental extensions"
