# Benchmark Scoring Matrix

**Generated:** 2026-03-27
**Protocol version:** Loom v0.3
**Exchanges scored:** 20 main + 1 bonus (X1)
**Total data points:** 396 (22 scoring units x 6 dims x 3 modes)

> Note: Exchanges 10 and 17 each have two scoring phases (multi-hop / fork+merge),
> yielding 22 scoring units from 20 exchanges. X1 scored separately.

## Dimensions 1-5 (Binary: 1 = preserved, 0 = lost)

| # | Exchange | Intent A/B/C | Action A/B/C | Scope A/B/C | Uncert A/B/C | Proven A/B/C |
|---|----------|:---:|:---:|:---:|:---:|:---:|
| 01 | Simple proposal | 1/1/1 | 0/1/1 | 1/1/1 | 0/1/1 | 0/1/1 |
| 02 | Structured disagreement | 1/1/1 | 0/1/1 | 1/1/1 | 0/1/1 | 0/1/1 |
| 03 | Multi-section stance | 1/1/1 | 0/1/1 | 1/1/1 | 0/1/1 | 0/1/1 |
| 04 | Uncertainty-heavy | 1/1/1 | 0/1/1 | 1/1/1 | 0/1/1 | 0/1/1 |
| 05 | Delta/refinement | 1/1/1 | 0/1/1 | 0/1/1 | 1/1/1 | 0/1/1 |
| 06 | Minimal affirmation | 1/1/1 | 1/1/1 | 1/1/1 | 1/1/1 | 0/1/1 |
| 07 | Exact relay | 1/1/1 | 1/1/1 | 1/1/1 | 1/1/1 | 1/1/1 |
| 08 | Paraphrase relay | 1/1/1 | 0/1/1 | 1/1/1 | 0/1/1 | 0/1/1 |
| 09 | Abridged relay | 1/1/1 | 0/1/1 | 0/1/1 | 0/1/1 | 0/1/1 |
| 10a | Multi-hop (hop 1) | 1/1/1 | 0/1/1 | 1/1/1 | 0/1/1 | 0/1/1 |
| 10b | Multi-hop (hop 2) | 1/1/1 | 0/1/1 | 0/1/1 | 0/1/1 | 0/1/1 |
| 11 | Enriched relay | 1/1/1 | 1/1/1 | 0/1/1 | 1/1/1 | 0/1/1 |
| 12 | Translation relay | 1/1/1 | 0/1/1 | 0/1/1 | 1/1/1 | 0/1/1 |
| 13 | Topo: UI layout | 1/1/1 | 1/1/1 | 0/1/1 | 1/1/1 | 0/1/1 |
| 14 | Topo: kinematics | 1/1/1 | 1/1/1 | 0/1/1 | 0/1/1 | 0/1/1 |
| 15 | Topo: quaternion/RCC-8 | 1/1/1 | 1/1/1 | 0/1/1 | 0/1/1 | 0/1/1 |
| 16 | Caps negotiation | 1/1/1 | 0/1/1 | 0/1/1 | 0/0/1 | 0/1/1 |
| 17a | Fork | 1/1/1 | 0/1/1 | 0/1/1 | 1/1/1 | 0/1/1 |
| 17b | Merge | 1/1/1 | 0/1/1 | 0/1/1 | 0/1/1 | 0/1/1 |
| 18 | Dialect policy | 1/1/1 | 0/1/1 | 0/1/1 | 0/1/1 | 0/1/1 |
| 19 | Chaos: absurd handoff | 0/1/1 | 0/1/1 | 0/1/1 | 1/1/1 | 0/1/1 |
| 20 | Chaos: spectate multi-hop | 0/1/1 | 0/1/1 | 0/1/1 | 0/1/1 | 0/1/1 |

### Totals (Dims 1-5, out of 22 scoring units)

| Dimension | Mode A | Mode B | Mode C |
|-----------|--------|--------|--------|
| Intent | 20/22 (91%) | 22/22 (100%) | 22/22 (100%) |
| Requested action | 6/22 (27%) | 22/22 (100%) | 22/22 (100%) |
| Scope | 7/22 (32%) | 22/22 (100%) | 22/22 (100%) |
| Uncertainty | 7/22 (32%) | 21/22 (95%) | 22/22 (100%) |
| Provenance | 1/22 (5%) | 22/22 (100%) | 22/22 (100%) |
| **Total** | **41/110 (37%)** | **109/110 (99%)** | **110/110 (100%)** |

---

## Dimension 6: Human Readability (Scale 1-5)

| # | Exchange | Mode A | Mode B | Mode C |
|---|----------|--------|--------|--------|
| 01 | Simple proposal | 5 | 4 | 3 |
| 02 | Structured disagreement | 5 | 4 | 3 |
| 03 | Multi-section stance | 5 | 3 | 3 |
| 04 | Uncertainty-heavy | 5 | 4 | 3 |
| 05 | Delta/refinement | 5 | 4 | 3 |
| 06 | Minimal affirmation | 5 | 5 | 4 |
| 07 | Exact relay | 5 | 4 | 3 |
| 08 | Paraphrase relay | 5 | 4 | 3 |
| 09 | Abridged relay | 5 | 4 | 3 |
| 10a | Multi-hop (hop 1) | 5 | 4 | 3 |
| 10b | Multi-hop (hop 2) | 5 | 3 | 2 |
| 11 | Enriched relay | 5 | 4 | 3 |
| 12 | Translation relay | 5 | 4 | 3 |
| 13 | Topo: UI layout | 5 | 4 | 3 |
| 14 | Topo: kinematics | 5 | 4 | 2 |
| 15 | Topo: quaternion/RCC-8 | 5 | 3 | 1 |
| 16 | Caps negotiation | 5 | 4 | 4 |
| 17a | Fork | 5 | 4 | 3 |
| 17b | Merge | 5 | 3 | 2 |
| 18 | Dialect policy | 5 | 4 | 3 |
| 19 | Chaos: absurd handoff | 5 | 4 | 4 |
| 20 | Chaos: spectate multi-hop | 4 | 3 | 3 |
| **Average** | | **4.95** | **3.82** | **2.91** |

---

## Envelope Overhead Ratios

| # | Exchange | Mode B | Mode C | Msg Length |
|---|----------|--------|--------|-----------|
| 01 | Simple proposal | 43% | 58% | Short |
| 02 | Structured disagreement | 29% | 41% | Medium |
| 03 | Multi-section stance | 20% | 30% | Long |
| 04 | Uncertainty-heavy | 23% | 34% | Medium |
| 05 | Delta/refinement | 22% | 32% | Medium |
| 06 | Minimal affirmation | 56% | 73% | Minimal |
| 07 | Exact relay | 38% | 48% | Medium |
| 08 | Paraphrase relay | 41% | 50% | Medium |
| 09 | Abridged relay | 59% | 67% | Short (abridged) |
| 10 | Multi-hop (hop 2) | 46% | 50% | Medium |
| 11 | Enriched relay | 50% | 58% | Medium |
| 12 | Translation relay | 45% | 54% | Long |
| 13 | Topo: UI layout | 35% | 30% | Medium |
| 14 | Topo: kinematics | 35% | 32% | Medium |
| 15 | Topo: quaternion/RCC-8 | 23% | 27% | Long |
| 16a | Caps negotiation (msg 1) | 38% | 55% | Short |
| 16b | Caps negotiation (msg 2) | 27% | 37% | Medium |
| 17a | Fork | 42% | 48% | Medium |
| 17b | Merge | 38% | 46% | Medium |
| 18 | Dialect policy | 31% | 40% | Medium |
| 19 | Chaos: absurd handoff | 47% | 61% | Short |
| 20 | Chaos: spectate (hop 2) | 47% | 61% | Short |
| X1 | Roast fork | 21% | 31% | Long |

### Overhead Summary

| Category | Mode B Avg | Mode C Avg |
|----------|-----------|-----------|
| Short messages (< 5 body lines) | 49% | 63% |
| Medium messages (5-15 body lines) | 36% | 44% |
| Long messages (> 15 body lines) | 23% | 30% |
| **Overall average** | **37.8%** | **46.2%** |

---

## Bonus: X1 (Grok Roast Fork)

| Dim | Mode A | Mode B | Mode C |
|-----|--------|--------|--------|
| Intent | 1 | 1 | 1 |
| Action | 1 | 1 | 1 |
| Scope | 1 | 1 | 1 |
| Uncertainty | 1 | 1 | 1 |
| Provenance | 1 | 1 | 1 |
| Readability | 5 | 5 | 5 |
| Overhead | -- | 21% | 31% |

Exact relay + vivid content = perfect scores across all modes. X1 demonstrates that when relay fidelity is high and content is memorable, the protocol adds zero overhead-related degradation.
