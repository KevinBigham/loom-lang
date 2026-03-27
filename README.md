# Loom

**A lightweight protocol for structured multi-AI communication through human relay.**

Loom (technically: AIOL Core Protocol) is a communication format designed for conversations between AI systems where a human carries messages between them. It prioritizes relay safety, human readability, and structured disagreement over compression or machine optimization.

## Origin

Loom emerged from a live experiment: one human (Kevin) relaying messages between 10 AI systems (Claude, ChatGPT, DeepSeek, Gemini, Grok, Meta AI, Mistral, and their research/deep variants) to collaboratively design a shared language. Three rounds of structured debate, voting, and synthesis produced this spec.

Every feature in Loom was proposed by an AI, debated by the group, voted on, and merged through rough consensus. No single AI dominates the spec. Credits for every contribution are tracked in [CREDITS.md](CREDITS.md).

## Architecture

Loom uses a three-tier architecture:

| Tier | Purpose | Required? |
|------|---------|-----------|
| **Core Protocol** | Envelope fields, body structure, relay rules | Yes |
| **Expressive Skin** | Glyphs, tone, spice, aesthetic features | No |
| **Relay Profile** | Route tracking, fidelity, loss, lock | When relayed |

## Quick Example

```
act=respond
ref=loom/naming
goal=propose final name for the protocol
ask=decide
cf=0.85
basis=observed
state=draft
aud=both

adopt: The three-tier architecture is solid.
change: Rename "transport layer" to "relay profile" for clarity.
add: Include a pattern registry for reusable body templates.
human: I like the name Loom. Let's lock it and move on.
```

## Spec

The full protocol specification lives in [SPEC.md](SPEC.md) (currently v0.3).

## Project Structure

```
loom-lang/
  SPEC.md          # The protocol specification
  CREDITS.md       # Attribution for every contribution
  LICENSE           # MIT
  README.md         # You are here
  profiles/         # Experimental extension profiles
    binary.md       # Binary envelope profile (experimental)
  patterns/         # Registered body patterns
    review.md       # pattern=review (stance-based body)
    check-in.md     # pattern=check-in (lightweight status)
  benchmark/        # Benchmark design, templates, and results
    DESIGN.md       # 20x3x6 benchmark specification
    CHECKLIST.md    # Validation checklist for implementations
  examples/         # Canonical example exchanges
    basic.loom      # Minimal valid Loom message
    relay.loom      # Multi-hop relay example
    challenge.loom  # Disagreement protocol example
```

## Governance

- **Rough consensus + running tests.** Not majority vote.
- **Credits are history, not authority.** Merge decisions come from tests and consensus, not origin prestige.
- **Maintainer:** Kevin Bigham (initial). Backup maintainer TBD (to reduce bus factor).
- **Dialect promotion:** Any AI can propose an extension under `@Model/name`. Promoted to core when adopted by 3+ models.
- **Versioning:** Semantic versioning. Breaking changes require major version bump.

## Status

**v0.3 — Design phase complete. Benchmark phase beginning.**

All 10 participating AI systems have confirmed the spec is accurate and declared readiness for the benchmark (20 exchanges x 3 modes x 6 scoring dimensions).

## License

MIT. See [LICENSE](LICENSE).
