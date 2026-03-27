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

The full protocol specification lives in [SPEC.md](SPEC.md) (currently v0.4).

## Roadmap

The post-benchmark convergence path lives in [ROADMAP.md](ROADMAP.md). Real-world evidence capture starts in [corpus/README.md](corpus/README.md), and known doc/spec mismatches are tracked in [governance/SPEC-DRIFT.md](governance/SPEC-DRIFT.md).

## Project Structure

```
loom-lang/
  ROADMAP.md       # Evidence-ladder roadmap from v0.5 to v1.0
  SPEC.md          # The protocol specification
  CREDITS.md       # Attribution for every contribution
  LICENSE           # MIT
  README.md         # You are here
  corpus/          # Real-world usage evidence for v0.5+
    README.md      # Corpus goals and workflow
    evidence.schema.json  # Exchange-level metadata schema
    real-world/    # Live Loom traffic captured for evidence
  governance/      # Release gates and drift tracking
    SPEC-DRIFT.md  # Known spec/grammar/example mismatches
  profiles/         # Experimental extension profiles
    binary.md       # Binary envelope profile (experimental)
  patterns/         # Registered body patterns
    review.md       # pattern=review (stance-based body)
    check-in.md     # pattern=check-in (lightweight status)
    CANDIDATES.md   # Probationary patterns awaiting live evidence
  benchmark/        # Benchmark design, execution, and results
    DESIGN.md       # 20x3x6 benchmark specification
    CHECKLIST.md    # Validation checklist for implementations
    RESULTS.md      # Full benchmark results and analysis
    scoring/        # Aggregated scoring matrix
    exchanges/      # All 21 exchange files (01-20 + X1)
  grammar/          # Protocol grammar
    ABNF.md         # Non-normative ABNF appendix (extracted from benchmark)
  examples/         # Canonical example exchanges
    basic.loom      # Minimal valid Loom message
    relay.loom      # Multi-hop relay example
    challenge.loom  # Disagreement protocol example
    governance-proposal.loom  # Dogfood template for protocol discussion
```

## Governance

- **Rough consensus + running tests.** Not majority vote.
- **Credits are history, not authority.** Merge decisions come from tests and consensus, not origin prestige.
- **Maintainer:** Kevin Bigham (initial). Backup maintainer TBD (to reduce bus factor).
- **Dialect promotion:** Any AI can propose an extension under `@Model/name`. Promoted to core when adopted by 3+ models.
- **Versioning:** Semantic versioning. Breaking changes require major version bump.

## Benchmark Results

The Loom v0.3 benchmark tested 20 exchanges across 3 communication modes on 6 scoring dimensions (360 data points). Full results: [benchmark/RESULTS.md](benchmark/RESULTS.md).

| Finding | Detail |
|---------|--------|
| **Core + Relay fidelity** | 99% (vs 37% for plain English) |
| **Most valuable field** | `ask=` (+73% action preservation) |
| **Biggest gap** | Provenance — 5% survival in plain English, 100% with Loom |
| **Human readability** | 3.8/5 for Core + Relay (passes 3.0 threshold) |
| **Overhead trade-off** | 49% for short messages, 23% for long — acceptable for the fidelity gain |

## Status

**v0.4 — Benchmark complete. Real-world usage phase.**

Benchmark results are in. The protocol works — structured communication dramatically outperforms plain English under human-relay conditions. v0.4 incorporates benchmark findings: new `enrich:` body section, mode guidance, intent inversion documentation, and a non-normative ABNF grammar appendix. The next phase is live dogfooding plus evidence capture for `v0.5`, using the corpus workflow and roadmap now tracked in-repo.

## License

MIT. See [LICENSE](LICENSE).
