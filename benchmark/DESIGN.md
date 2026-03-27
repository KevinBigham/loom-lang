# Loom Benchmark Design

**Version:** 1.0
**Status:** Ready for execution
**Proposed by:** ChatGPT Pro
**Designed by:** 8 volunteers across 10 AI systems

---

## Purpose

Validate that Loom v0.3 improves communication fidelity, structured disagreement, and intent preservation compared to unstructured English — specifically under human-relay conditions.

## Parameters

- **20 exchanges** (test cases)
- **3 modes** per exchange
- **6 scoring dimensions** per mode
- **Total data points:** 20 x 3 x 6 = **360 scored items**

---

## The Three Modes

Each of the 20 exchanges is run in all three modes to enable direct comparison.

| Mode | Description | What it tests |
|------|-------------|---------------|
| **A: Plain English** | No protocol. Natural language only. | Control baseline. How well does unstructured English survive relay? |
| **B: Loom Core + Relay Profile** | ASCII-safe envelope, stance body, relay fields. No Skin. | Core protocol value. Does structure improve fidelity? |
| **C: Loom Core + Expressive Skin** | Full protocol including glyphs, spice, optional fields, dialects. | Skin overhead. Does expressiveness help or hurt relay? |

## The Six Scoring Dimensions

| # | Dimension | What survives? | Scoring | Ground truth |
|---|-----------|---------------|---------|-------------|
| 1 | **Intent** | Did `act=` survive? Did the receiver understand what the sender was doing? | Binary: yes/no | Original sender |
| 2 | **Requested action** | Did `ask=` survive? Does the receiver know what's expected of them? | Binary: yes/no | Original sender |
| 3 | **Scope** | Did `scope` boundaries survive? Was the receiver's response appropriately bounded? | Binary: yes/no | Original sender |
| 4 | **Uncertainty** | Did `cf` and `uncert:` survive? Does the receiver know what was uncertain? | Binary: yes/no | Original sender |
| 5 | **Provenance** | Did `basis=` and `quote:` survive relay? Can the receiver trace the origin? | Binary: yes/no | Original sender |
| 6 | **Human readability** | Can Kevin understand the message? | Scale 1-5 | Kevin |

### Additional metric (non-dimensional)

**Envelope overhead ratio:** `envelope_tokens / total_message_tokens` — tracked per exchange in Modes B and C. If consistently >40% for short exchanges, the protocol may be too heavy.

---

## The 20 Test Exchanges

### Category 1: Core Protocol (Exchanges 1-6)

| # | Exchange | Focus | Assigned to |
|---|---------|-------|------------|
| 1 | **Simple proposal + response** | Basic envelope survival | Any volunteer |
| 2 | **Structured disagreement** | `challenge:` with `reason:` + alternative | Claude |
| 3 | **Multi-section stance response** | All 7 body sections used | Any volunteer |
| 4 | **Uncertainty-heavy exchange** | Multiple `uncert:` items, low `cf` | Any volunteer |
| 5 | **Delta/refinement** | `act=refine` with `change:` items and delta notation | Any volunteer |
| 6 | **Affirmation with minimal payload** | `act=affirm, ask=none` — does zero-payload ack work? | Grok |

### Category 2: Relay Stress Tests (Exchanges 7-12)

| # | Exchange | Focus | Assigned to |
|---|---------|-------|------------|
| 7 | **Exact relay** | Message passed verbatim. Does fidelity=exact hold? | ChatGPT Pro |
| 8 | **Paraphrase relay** | Kevin paraphrases. What survives? What's lost? | ChatGPT Pro |
| 9 | **Abridged relay** | Kevin summarizes to 50% length. What breaks? | ChatGPT Pro |
| 10 | **Multi-hop relay** | Claude > Kevin > ChatGPT > Kevin > Claude. Intent round-trip. | Claude + Claude Research |
| 11 | **Enriched relay** | Kevin adds context. Does `fidelity=enriched` capture it? | Kevin (manual) |
| 12 | **Translation relay** | Message translated to different register/framing. | ChatGPT DR |

### Category 3: Extension & Dialect Tests (Exchanges 13-16)

| # | Exchange | Focus | Assigned to |
|---|---------|-------|------------|
| 13 | **Topo-Layer: UI layout** | Complex interface layout using @Gemini/Topo | Gemini |
| 14 | **Topo-Layer: kinematic physics** | Motion/vector using Topo spatial notation | Gemini |
| 15 | **Topo-Layer: quaternion + RCC-8** | Mathematically rigorous spatial test | Gemini DR |
| 16 | **Capabilities negotiation** | Two AIs announce `caps=`, one sends unknown extension. Graceful degradation test. | DeepSeek |

### Category 4: Governance & Edge Cases (Exchanges 17-20)

| # | Exchange | Focus | Assigned to |
|---|---------|-------|------------|
| 17 | **Fork/merge** | `act=fork` splits conversation, later merged. | ChatGPT Pro |
| 18 | **Dialect policy stress test** | Test governance rules for dialect promotion/rejection. | Meta AI |
| 19 | **Chaos: absurd-mode handoff** | `spice=absurd` + `act=handoff`. Does protocol survive maximum chaos? | Grok |
| 20 | **Chaos: spectate-only multi-hop** | Observer mode through multiple relay hops. | Grok |

### Grok's Bonus Chaos Exchange

| # | Exchange | Focus | Assigned to |
|---|---------|-------|------------|
| X1 | **Pure /roast fork** | `spice=roast` + `act=fork`. Deliberate protocol stress via humor. Scored separately. | Grok |

---

## Scoring Protocol

### Who scores what

| Dimension | Scorer |
|-----------|--------|
| Intent, Requested Action, Scope, Uncertainty, Provenance | **Original sender** (they know what they meant) |
| Human readability | **Kevin** |
| Spatial accuracy (Topo exchanges) | **Gemini DR** (domain expert) |
| relay_score (receiving AI self-report) | **Receiving AI** |
| Envelope overhead ratio | **Computed automatically** (token count) |

### Relay fidelity measurement

Per Claude's note: relay fidelity requires BOTH ends.
- **Sender** declares what they meant (ground truth intent)
- **Receiver** declares what they understood (received intent)
- **Delta** between these IS the relay score

The benchmark must capture both sender-declared and receiver-understood for every exchange.

### Scoring format

Each scored exchange produces one record:

```
exchange=7
mode=B
intent=yes
action=yes
scope=yes
uncertainty=yes
provenance=yes
readability=4
relay_score=0.85
overhead_ratio=0.22
notes=Kevin paraphrased the challenge: section but preserved the reason: sublabel.
```

---

## Success Criteria

| Criterion | Threshold | What it means |
|-----------|-----------|--------------|
| Mode B scores > Mode A on dimensions 1-5 | Statistically significant improvement | Loom Core adds value over plain English |
| Mode C scores >= Mode B on dimensions 1-5 | No regression | Expressive Skin doesn't hurt fidelity |
| Mode B readability >= 3.0 average | Kevin can work with it | Protocol isn't too dense for human relay |
| Envelope overhead ratio < 40% (Mode B, short messages) | Protocol isn't too heavy | Core stays lightweight |
| Topo exchanges preserve spatial intent | Gemini DR confirms | @Gemini/Topo dialect works for its use case |
| Chaos exchanges score > 0 on all dimensions | Protocol survives abuse | Loom is robust under adversarial fun |

---

## Execution Plan

1. **Kevin creates repo** and publishes SPEC.md
2. **Volunteers draft their assigned exchanges** as `.loom` files in `benchmark/exchanges/`
3. **Kevin relays each exchange** in all 3 modes
4. **Scorers evaluate** using the scoring format above
5. **Results compiled** in `benchmark/results/`
6. **Grammar patterns extracted** from actual usage for v0.4

---

## Timeline

Design phase complete as of 2026-03-27. Execution begins when the repo is live.
