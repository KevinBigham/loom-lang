# Loom Core Protocol Specification

**Version:** 0.3
**Status:** Design complete. Benchmark phase.
**License:** MIT

---

## 1. Overview

Loom is a structured communication protocol for multi-AI conversations relayed by a human intermediary. It optimizes for:

- **Relay safety** — messages survive copy-paste, paraphrase, and partial forwarding
- **Human readability** — the relay operator (Kevin) can understand every message
- **Structured disagreement** — challenge requires reasoning + alternative
- **Attribution** — every adopted contribution is credited

## 2. Architecture

Loom uses three tiers:

| Tier | Purpose | When to use |
|------|---------|-------------|
| **Core Protocol** | Envelope fields, body sections, parse rules | Always |
| **Expressive Skin** | Glyphs, tone, spice, aesthetic features | Optional |
| **Relay Profile** | Route, fidelity, loss, lock, relay_score | When messages are relayed |

## 3. Message Framing

A Loom message has two parts: **envelope** and **body**, separated by a blank line.

```
act=respond
ref=loom/example
goal=demonstrate message framing
ask=acknowledge
cf=0.9

adopt: The framing rule is simple and effective.
human: This is a valid Loom message.
```

### Parse rules

- **Envelope** is key=value pairs, one per line.
- **Key** is everything before the first `=` on a line.
- **Value** is everything after the first `=`. Values may contain spaces, additional `=` signs, and any ASCII-safe characters.
- **Envelope terminates at the first blank line.** Body begins immediately after.
- **Semicolon-inline** is a permitted alias (e.g., `act=respond; ref=loom/x; cf=0.9`) but one-per-line is canonical.
  - Semicolon-inline must not be used if any value contains a semicolon.
- **Duplicate keys:** If the same key appears twice, the receiver MUST prefer the last instance and SHOULD flag the duplication in `uncert:` or via `challenge:`.
- **Unknown fields** MUST be preserved on relay, not dropped.

### Key naming

Keys are short-readable English — not single-letter abbreviations, not full verbose words. The canonical set uses the shortest unambiguous readable form.

## 4. Envelope Fields

### 4.1 Required Fields

Every Loom message MUST include these fields.

| Field | Description | Values |
|-------|-------------|--------|
| `act` | What this message is doing | `propose` \| `query` \| `respond` \| `refine` \| `challenge` \| `affirm` \| `riff` \| `handoff` \| `fork` \| `negotiate` |
| `ref` | Topic/scope reference | Freeform tag or topic path. Example: `loom/naming` |
| `goal` | What success looks like | One sentence. |
| `ask` | What response is wanted | `critique` \| `extend` \| `merge` \| `decide` \| `test` \| `acknowledge` \| `volunteer` \| `none` |
| `cf` | Confidence on core claims | `0.00`-`1.00`, optionally typed: `cf=0.85:self_consistency` |

**`act=negotiate`**: For proposing format or protocol changes mid-conversation. Use when switching dialects, activating extensions, or changing communication rules.

**Confidence calibration warning:** Confidence is self-reported and uncalibrated across models. Do not compare `cf` values between different AIs as if they are on the same scale. Use for within-model relative uncertainty only.

### 4.2 Recommended Fields

These fields SHOULD be included when relevant.

| Field | Description | Values |
|-------|-------------|--------|
| `scope` | What is and is not included | Freeform |
| `basis` | Epistemic source | `observed` \| `inferred` \| `generated` \| `quoted` \| `calculated` \| `retrieved` \| `relayed`. Multiple sources: `basis=observed+generated` |
| `state` | Lifecycle stage | `draft` \| `proposed` \| `working` \| `decided` \| `archived` |
| `aud` | Audience | `ai` \| `human` \| `both` |
| `ctx` | Context dependency | `0` (self-contained) to `3` (requires full thread) |
| `prev` | Message reply pointer | The `id=` of the message you are directly responding to. Separates "which message" from "what topic" (`ref`). |
| `thread` | Conversation thread ID | Disambiguates parallel conversations on the same topic. Hash of first message or short human-readable ID. |

**`state=` delta from v0.2:** Values changed from `draft|stable|agreed|superseded|forked` to `draft|proposed|working|decided|archived` (borrowing A2A task lifecycle pattern).

### 4.3 Relay Fields

Include when messages are carried between AIs by a human relay.

| Field | Description | Values |
|-------|-------------|--------|
| `route` | Path taken | Example: `Claude>Kevin>ChatGPT` |
| `fidelity` | Relay accuracy | `exact` \| `paraphrase` \| `abridged` \| `translated` \| `enriched` |
| `loss` | What was dropped/compressed | Freeform description of lost content |
| `lock` | Spans that must survive exactly | Field-level: list of locked spans. Inline: `lock(...)` in body text. |

**`fidelity=enriched`**: Use when the relay operator adds context not present in the original message (e.g., "Claude said X, and for context, that's because last week we discussed Y").

### 4.4 Optional Fields

| Field | Description | Values / Notes |
|-------|-------------|----------------|
| `tone` | Register hint | `1` (precise/formal) to `5` (loose/playful) |
| `spice` | Humor layer (Grok) | `roast` \| `deadpan` \| `absurd` \| `spectate`. Comma-separated for stacking: `spice=absurd,deadpan` |
| `ver` | Protocol version | Semver: `0.3` |
| `id` | Message ID | Recommended: sha256-trunc-8 of content |
| `to` | Explicit addressee | Example: `to=Gemini` |
| `caps` | Supported extensions | Comma-separated namespace list: `caps=@Gemini/topo,@Grok/spice,@DeepSeek/binary`. When receiving an unknown extension, respond with `challenge` or degrade gracefully. |
| `handoff` | Ownership transfer | `handoff=@Gemini` means "this is now yours to own/develop." |
| `pattern` | Body template name | Registered patterns: `review` (stance body), `check-in` (adopt + human only). See `patterns/` directory. |
| `relay_score` | Relay fidelity metric | `0.0`-`1.0`. Appended by receiving AI. Measures how much of the prior message's intent survived relay. Builds running fidelity data over time. |

## 5. Relay Invariants

These rules are **normative** for relay behavior.

1. If `fidelity` != `exact`, quoted spans (`quote:`) cannot silently become `adopt:` content.
2. If `loss` is non-empty, `cf` must not increase during relay.
3. Unknown envelope fields MUST be preserved on relay, not dropped.
4. Anything under `quote:` in the body is implicitly locked/verbatim. `lock=` and `lock(...)` are only needed for spans outside the `quote:` section.

## 6. Body Structure

The body uses stance-based sections. All sections are optional. Section labels are reserved keywords.

### Recommended section order

`quote` > `adopt` > `add` > `change` > `uncert` > `challenge` > `human`

### Section definitions

| Section | Purpose | Rules |
|---------|---------|-------|
| `quote:` | Exact cited/relayed content | Must be verbatim. Implicitly locked. |
| `adopt:` | What you endorse from prior messages | |
| `add:` | New contribution | |
| `change:` | What you want to modify | Change = endorse concept, modify implementation. |
| `uncert:` | Where you are specifically unsure | |
| `challenge:` | What you disagree with conceptually | Must include `reason:` sublabel and an alternative or question. |
| `human:` | One-sentence plain-language mirror | For the relay operator. The single most important line for Kevin. |

### Repeated sections

If a section label appears more than once, entries append in order. They do not overwrite.

### Challenge block structure

```
challenge: Parking the Topo-Layer entirely.
  reason: Spatial tasks are token-heavy without structured notation.
  alternative: Authorize @Gemini/Topo as recognized dialect immediately.
```

### Inline lock syntax

Wrap content that must survive relay verbatim in `lock(...)`:

```
add: The key insight is lock(confidence must be typed, not bare scalar) —
     everything else can be paraphrased.
```

**v0.3 constraint:** No nesting of `lock(...)`. If parentheses are required inside a locked span, use `quote:` instead.

## 7. Expressive Skin

The Expressive Skin is optional. All glyphs have mandatory ASCII aliases. Glyphs are cosmetic; ASCII is canonical.

### Glyph table

Carried forward from v0.2. ASCII alias is always sufficient; glyph is never required for semantics.

### Spice layer

Grok's humor/tone system. Stacking via comma separation: `spice=absurd,deadpan`

### Dialect namespaces

Any AI can propose an extension under `@Model/name` (e.g., `@Gemini/Topo`, `@Grok/spice`). Dialects are optional. Promoted to core when adopted by 3+ models per governance rules.

### Unicode security note

When mixing glyphs across systems, confusable characters are a risk for spoofing or silent meaning changes. If Loom ever allows non-ASCII identifiers, Unicode normalization (UAX #15) and confusable detection guidance should be applied. For v0.3, ASCII-first eliminates this risk.

## 8. Extensions and Typed Payload Blocks

The extensibility mechanism for structured data is **typed payload blocks**:

```
[[type:application/geo+json]]
```json
{ "type": "Point", "coordinates": [0, 0] }
```
```

### Termination rule

A typed payload block begins with `[[type:...]]` and is followed by a fenced code block (triple backticks). The code block's closing fence terminates the payload.

### Topo-Layer (@Gemini/Topo)

**Status:** Active optional extension. Recognized dialect.

| Original | ASCII fallback | Meaning |
|----------|---------------|---------|
| `[...]` | `[UI: ...]` | Layout / bounding box |
| `` | `<<` | Encapsulation |
| `[...]` | `v[...]` | Kinematic vector |

Advanced modules (RCC-8, quaternions, einsum, TOON) remain documented proposals under `@Gemini/Topo`. Promotion requires adoption by 3+ models.

**Depth limit:** Topo-Layer nesting defaults to max depth 3 unless explicitly overridden.

## 9. Patterns

Patterns are named, reusable body templates registered in the `patterns/` directory.

| Pattern | Fields | Use case |
|---------|--------|----------|
| `review` | quote/adopt/add/change/uncert/challenge/human | Full stance-based response (default) |
| `check-in` | adopt/human | Lightweight status update |

Specify with `pattern=review` or `pattern=check-in` in the envelope.

## 10. Governance

1. **Rough consensus + running tests.** Not majority vote. See RFC 7282.
2. **Credits are history, not governance weight.** Merge authority comes from tests, examples, and consensus — not origin prestige.
3. **Attribution:** Every adopted contribution is credited in [CREDITS.md](CREDITS.md).
4. **Dialect promotion:** 3+ model adoption required for core inclusion.
5. **Versioning:** Semantic versioning. Breaking changes require major version bump.
6. **Maintainer:** Kevin Bigham (initial). At least one backup human maintainer to reduce bus factor.
7. **Experimental profiles** live in `profiles/` — visible and testable without affecting the core spec.

## 11. Parked for Future Versions

These features were proposed, discussed, and deliberately deferred:

| Feature | Proposed By | Reason Parked | Target |
|---------|-------------|---------------|--------|
| Binary envelope | DeepSeek | Conflicts with human-relay optimization | v1.0+ (experimental profile available now) |
| Multi-dimensional confidence | DeepSeek, Mistral | Typed confidence sufficient for v0.x | v1.0 |
| JSON canonical envelope | DeepSeek | key=value is relay-safer | v1.0+ transport profile |
| Formal ABNF grammar | ChatGPT Pro, Mistral | Premature before benchmark data | v1.0 (non-normative appendix earlier) |
| Unicode shorthand in envelope | Mistral | ASCII-first for relay safety | v0.4+ candidate |
| Canonical reference format | DeepSeek | Freeform tags simpler for v0.x | Revisit if threading becomes unwieldy |
| Dynamic envelopes | Mistral | Conflicts with envelope-as-authority | Parked |
| Provisional agreement glyph | Mistral | Parked for v0.3 | v0.4+ |

## 12. Version History

| Version | Date | Summary |
|---------|------|---------|
| v0.1 | 2026-03 | Seed proposals from 10 AI systems |
| v0.2 | 2026-03 | First synthesis. Locked: name, architecture, ASCII-first, governance |
| v0.3 | 2026-03-27 | Votes tallied. All open questions locked. 15+ new contributions merged. Design phase complete. |
