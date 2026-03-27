# Loom v0.3 Benchmark Results

**Date:** 2026-03-27
**Protocol version:** v0.3
**Benchmark design:** 20 exchanges x 3 modes x 6 dimensions = 360 scored items (+ bonus X1)
**Scoring units:** 22 (exchanges 10 and 17 each have two scored phases)

---

## Executive Summary

Loom v0.3 dramatically improves structured communication fidelity under human-relay conditions. The protocol's core value proposition is confirmed: **structured envelope fields survive relay where unstructured prose does not.**

| Metric | Result | Verdict |
|--------|--------|---------|
| Mode B > Mode A (dims 1-5) | 99% vs 37% | **PASS** |
| Mode C >= Mode B (dims 1-5) | 100% vs 99% | **PASS** |
| Mode B readability >= 3.0 | 3.82 avg | **PASS** |
| Envelope overhead < 40% (short msgs) | 49% avg for short | **FAIL** |
| Topo preserves spatial intent | 3/3 exchanges pass | **PASS** |
| Chaos exchanges > 0 all dims | Yes | **PASS** |

**5 of 6 success criteria met.** The one failure (short-message overhead) is a known trade-off with a clear mitigation path (pattern=check-in, envelope compression for v0.4).

---

## Detailed Results

### 1. Content Fidelity (Dimensions 1-5)

**Mode A (Plain English):** 41/110 = 37.3%
**Mode B (Loom Core + Relay):** 109/110 = 99.1%
**Mode C (Loom Core + Skin):** 110/110 = 100%

The gap between Mode A and Mode B is the protocol's core contribution. Breaking it down by dimension:

| Dimension | Mode A | Mode B | Mode C | Gap (A→B) |
|-----------|--------|--------|--------|-----------|
| Intent preserved | 91% | 100% | 100% | +9% |
| Requested action | 27% | 100% | 100% | **+73%** |
| Scope preserved | 32% | 100% | 100% | **+68%** |
| Uncertainty preserved | 32% | 95% | 100% | **+63%** |
| Provenance preserved | 5% | 100% | 100% | **+95%** |

**Key findings:**

- **Intent** is the most relay-resistant dimension even without protocol — it survives in plain English 91% of the time. The two failures (exchanges 19, 20) occurred when humor/spectate mode caused intent ambiguity.
- **Provenance** is the most relay-fragile dimension in plain English — only 5% survival. There is simply no natural-language mechanism for tracking epistemic source. The `basis=` field is transformative.
- **Requested action** improves the most dramatically (+73%). "Weigh in," "let me know what you think," and "thoughts?" are all ambiguous. `ask=decide` is not.
- **Mode B's single failure** (exchange 16, uncertainty) occurred because capability mismatch implied an uncertainty that wasn't explicitly flagged. Mode C's `uncert:` block caught it. This suggests `uncert:` is more important for extension-related messages.

### 2. Human Readability (Dimension 6)

| Mode | Average | Min | Max |
|------|---------|-----|-----|
| A | 4.95 | 4 | 5 |
| B | 3.82 | 3 | 5 |
| C | 2.91 | 1 | 5 |

**Mode B passes the 3.0 threshold** with room to spare. Kevin can work with Loom Core messages. The structured format becomes natural after brief exposure — the `human:` line is the critical accessibility feature.

**Mode C narrowly misses at 2.91.** The Expressive Skin adds metadata that helps AI receivers but taxes human comprehension. Three specific pain points:
- Exchange 15 (quaternion/RCC-8): readability = 1. Kevin cannot understand quaternion math — the protocol is copy-safe but not comprehension-safe for this content.
- Exchange 10b (multi-hop, hop 2): readability = 2. Accumulated relay metadata + skin metadata = cognitive overload.
- Exchange 17b (merge phase): readability = 2. Merge negotiation with thread IDs is dense.

**Recommendation:** Mode C should not be used for human-relayed messages unless the relay operator is technically literate. For Kevin's use case, Mode B is the sweet spot. Mode C is for direct AI-to-AI communication or archival.

### 3. Envelope Overhead

| Message Length | Mode B | Mode C | Threshold |
|---------------|--------|--------|-----------|
| Short (< 5 body lines) | **49%** | 63% | < 40% |
| Medium (5-15 body lines) | 36% | 44% | < 40% |
| Long (> 15 body lines) | **23%** | 30% | < 40% |
| Overall | 37.8% | 46.2% | < 40% |

**Short messages exceed the 40% threshold** for Mode B (49% average). This is the "short message penalty" — the fixed overhead of 5 required envelope fields dominates when the body is small.

**Medium and long messages are within threshold.** Mode B at 36% and 23% respectively shows the protocol becomes more efficient as content grows.

**Mitigations for v0.4:**
1. `pattern=check-in` already reduces body to adopt + human (2 sections). The envelope overhead for check-in style messages should be benchmarked separately.
2. Consider an envelope compression mode for short messages (e.g., semicolon-inline for messages under 3 body lines).
3. The overhead is a fair trade for the fidelity gains — 49% overhead that delivers 99% fidelity vs 0% overhead that delivers 37% fidelity.

### 4. Relay Stress Tests (Exchanges 7-12)

| Test | Key Finding |
|------|-------------|
| **07: Exact relay** | Baseline confirmed. All modes score 5/5 when Kevin copies verbatim. Protocol structure introduces no copy errors. |
| **08: Paraphrase** | **The critical test.** Envelope fields survive paraphrase intact. Kevin naturally preserves key=value pairs while rewording the body. Mode A loses 3 dimensions; Mode B loses 0. |
| **09: Abridged** | The `loss=` field is the hero. When Kevin cuts content, Mode B tells the receiver exactly what's missing. Mode A gives no indication of what was dropped. |
| **10: Multi-hop** | Cumulative degradation is real but documented. `route=` tracks the full path. `loss=` accumulates per hop. Mode A shows significant semantic drift by hop 2. |
| **11: Enriched** | **Protocol gap identified.** `fidelity=enriched` signals Kevin added context, but there's no body-level mechanism to separate original content from Kevin's additions. Recommending `enrich:` section for v0.4. |
| **12: Translation** | `fidelity=translated` honestly signals register shift. `tone=` quantifies the change. Technical substance survives register translation better in Mode B. |

**Relay stress summary:** Loom's relay fields (`route`, `fidelity`, `loss`, `lock`) are the protocol's most valuable innovation for the human-relay use case. They transform opaque degradation into documented, trackable degradation.

### 5. Extension & Dialect Tests (Exchanges 13-16)

| Test | Key Finding |
|------|-------------|
| **13: Topo UI layout** | @Gemini/Topo ASCII notation survives copy-paste. Kevin doesn't need to understand it — `[UI: ...]` is copy-safe. Spatial precision preserved. |
| **14: Topo kinematics** | Vector notation (`v[...]`) survives exact copy. Kevin's paraphrase drops numeric precision — this is expected and acceptable because the notation is designed for copy, not paraphrase. |
| **15: Topo quaternion/RCC-8** | Pushes human relay to its absolute limit. Kevin produces contradictory spatial claims in Mode A. Mode C's typed payload blocks preserve the math exactly. **Readability = 1** is acceptable — this content was never meant for human comprehension, only copy-safe transport. |
| **16: Caps negotiation** | `caps=` field enables capability discovery that Mode A fundamentally cannot do. Unknown extension preservation (relay invariant #3) works correctly. Mode C's explicit `uncert:` about unsupported extensions is the only mode that scores 1/1 on uncertainty. |

**Extension summary:** The three-tier architecture works. Core handles simple exchanges, Skin handles metadata-rich ones, and typed payload blocks handle domain-specific content (math, spatial, code). Kevin doesn't need to understand every extension — he just needs to copy-paste faithfully.

### 6. Governance & Edge Cases (Exchanges 17-20)

| Test | Key Finding |
|------|-------------|
| **17: Fork/merge** | `act=fork` is unambiguous; prose "let's split this up" is not. The merge phase is the hardest — Mode A merge is unverifiable. `thread=` IDs make fork/merge trackable. |
| **18: Dialect policy** | Meta-governance (arguing about the protocol's rules through the protocol) works. Structured body separates claim from evidence. `basis=observed` grounds the argument in data. |
| **19: Chaos absurd handoff** | **Structure separates intent from expression.** `act=handoff` is unambiguous even when the body is absurd. In Mode A, humor masks the real handoff — the receiver genuinely doesn't know if Grok is serious. `spice=absurd` resolves this. |
| **20: Chaos spectate multi-hop** | **Largest scoring gap in the benchmark** (0/5 vs 5/5). Two hops of spectate mode in plain English = complete intent inversion (observation becomes proposal). `act=riff` + `ask=none` + `spice=spectate` makes passive intent tamper-proof. |

**Edge case summary:** The protocol's value is highest in ambiguous and complex scenarios — exactly where unstructured communication fails most catastrophically.

---

## Cross-Cutting Findings

### What Loom Does Best
1. **Preserving requested action** — `ask=` is the single highest-value field. +73% improvement over plain English.
2. **Preserving provenance** — `basis=` and `quote:` make epistemic tracking possible. +95% improvement.
3. **Documenting relay loss** — `loss=` transforms silent degradation into explicit, addressable gaps.
4. **Disambiguating intent under chaos** — `act=` + `spice=` separates what you're doing from how you're saying it.

### What Loom Struggles With
1. **Short message overhead** — The fixed 5-field envelope dominates minimal messages. `pattern=check-in` helps but doesn't fully solve it.
2. **Mode C readability** — Expressive Skin pushes human readability below 3.0. Not suitable for human-relayed messages without technical background.
3. **Enrichment attribution** — No body-level mechanism to separate relay-added content from original content.
4. **Multi-hop cumulative overhead** — Relay metadata accumulates across hops, degrading readability.

### Unexpected Discoveries
1. **Kevin naturally preserves key=value pairs** — When paraphrasing, Kevin rewrites prose but tends to copy structured fields intact. The envelope format leverages this human behavior.
2. **The `human:` line is the protocol's most important feature for the relay use case** — It gives Kevin a one-sentence summary he can always fall back on. Multiple exchanges showed Kevin's relay improving when `human:` was clear.
3. **Concrete examples are the most relay-resistant form of content** — Exchange 12 showed that locked code examples survive relay better than abstract explanations of the same concept.
4. **Exchange 20 revealed a new protocol property: "intent inversion"** — Over multiple hops without structure, passive observation can become active proposal. This is a previously undocumented failure mode that Loom prevents.

---

## Success Criteria Assessment

### PASS: Mode B > Mode A on dimensions 1-5
99.1% vs 37.3%. Not close. Loom Core adds enormous value.

### PASS: Mode C >= Mode B on dimensions 1-5
100% vs 99.1%. Mode C catches the one edge case (exchange 16 uncertainty) that Mode B misses. Marginal but consistent.

### PASS: Mode B readability average >= 3.0
3.82. Kevin can work with Loom Core. The `human:` line is key.

### FAIL: Envelope overhead < 40% for short messages (Mode B)
49% average for short messages. 37.8% overall. The overall average passes, but short messages specifically fail. This is an expected trade-off — the 5 required fields create a fixed floor. Mitigations recommended for v0.4.

### PASS: Topo exchanges preserve spatial intent
3/3 Topo exchanges (13, 14, 15) preserve spatial intent in Modes B and C. Mode A fails all three on scope. @Gemini/Topo notation works as designed — copy-safe even when the human relay doesn't understand the content.

### PASS: Chaos exchanges score > 0 on all dimensions
Exchanges 19 and 20 score > 0 on all dimensions in Modes B and C. Mode A fails multiple dimensions on both chaos exchanges, demonstrating that the protocol's value is highest precisely when communication is most chaotic.

---

## Recommendations for v0.4

Based on benchmark findings, the following changes are recommended:

### New Features
1. **`enrich:` body section** — For relay-added content. Solves the attribution gap found in exchange 11. Placed after `human:` in section order.
2. **Envelope compression mode** — Semicolon-inline for messages with <= 3 body lines. Opt-in via `compact=true` or by using semicolon-inline syntax.
3. **`relay_score=` promotion** — Currently optional. Should be recommended for multi-hop scenarios (exchange 10 showed its value).
4. **Multi-hop readability warning** — Suggest Mode B (not C) for messages expected to traverse > 1 hop.

### Spec Clarifications
5. **"Intent inversion" as named failure mode** — Document the exchange 20 finding: passive intent can invert over multiple hops without structural markers.
6. **Short message overhead guidance** — Acknowledge the trade-off in the spec. Recommend `pattern=check-in` for lightweight exchanges.
7. **Mode C audience guidance** — Explicitly note Mode C is optimized for AI receivers, not human relays.

### Grammar Patterns to Extract
8. **Envelope grammar** — 20 exchanges provide sufficient examples to draft a non-normative ABNF appendix for v0.4 (as the voted plan specified).
9. **Body section grammar** — Section label syntax, indentation rules, sublabel patterns (reason:, alternative:) are now well-exercised.
10. **Relay field grammar** — route, fidelity, loss patterns are stable across all relay stress tests.

---

## Data Files

- **Scoring matrix:** [scoring/matrix.md](scoring/matrix.md)
- **Individual exchanges:** [exchanges/01-simple-proposal.md](exchanges/01-simple-proposal.md) through [exchanges/X1-roast-fork.md](exchanges/X1-roast-fork.md)
- **Benchmark design:** [DESIGN.md](DESIGN.md)
- **Validation checklist:** [CHECKLIST.md](CHECKLIST.md)
