# Exchange 11: Enriched Relay

**Category:** Relay Stress Tests
**Tests:** `fidelity=enriched` -- can the receiver distinguish original content from Kevin's additions?
**Volunteer:** Kevin (manual)
**Relay type:** Enriched (Kevin adds context from his cross-AI knowledge)

---

## Sender: Mistral -> Kevin -> Claude

### Scenario

Mistral proposes revisiting Unicode shorthand for envelope fields. Kevin, who has been tracking all 10 AIs' positions across multiple rounds, adds context that no single AI has: DeepSeek mentioned something similar in Round 1 but with different syntax, and Gemini had concerns about rendering. Kevin enriches the message with cross-AI context. This tests whether fidelity=enriched correctly captures that Kevin added information, and whether the receiver can distinguish Mistral's original content from Kevin's additions.

---

### MODE A -- Plain English

**Original (Mistral):**
> I'd like to revisit the idea of Unicode shorthand for envelope fields. Right now, the envelope is ASCII-only, which keeps things safe but verbose. My proposal: allow an optional Unicode alias layer where common envelope patterns can use compact glyphs. For example, the confidence field could use a visual indicator alongside the numeric value, section labels could have compact prefixes, and the route field could use arrow characters instead of the > separator. This would be opt-in -- ASCII remains canonical, Unicode is a display optimization. I'm about 70% confident this improves readability without breaking anything, but I'm uncertain about cross-platform rendering consistency. Some terminals and chat interfaces mangle Unicode in unpredictable ways. I'd like critique on the trade-offs.

**Kevin's relay to Claude:**
> Mistral wants to bring back Unicode shorthand for envelope fields -- like using special characters instead of the verbose ASCII stuff. It'd be opt-in, ASCII stays the default. They're 70% on it but worried about rendering issues across platforms. Oh btw, DeepSeek actually proposed something similar back in Round 1 but with different syntax -- they wanted single-character aliases for act= values. And Gemini pushed back on anything Unicode because of terminal rendering problems in their Topo testing. So there's already some history here. Mistral wants critique.

**Claude receives and interprets:**
> Mistral proposes Unicode shorthand for envelope fields. Opt-in, ASCII stays canonical. Some history: DeepSeek proposed something similar before, Gemini had rendering concerns. Mistral is 70% confident. Wants critique.

### What Mode A lost / confused

- No way to tell which content is Mistral's and which is Kevin's. The DeepSeek and Gemini context appears as if it might have been in Mistral's original message.
- Claude might attribute the Round 1 / Gemini knowledge to Mistral, which would be incorrect provenance.
- If Claude responds referencing "Mistral's point about DeepSeek's syntax" -- that was Kevin's context, not Mistral's. This creates false attribution chains.
- Kevin's "bring back" framing implies this was previously discussed and rejected, which is Kevin's editorial interpretation, not Mistral's framing.

---

### MODE B -- Loom Core + Relay Profile

**Original (Mistral):**
```
act=propose
ref=loom/envelope/unicode-shorthand
goal=add optional Unicode alias layer for envelope field display
ask=critique
cf=0.70
basis=inferred+generated
state=draft

add: Allow optional Unicode alias layer for common envelope patterns.
     ASCII remains canonical; Unicode is a display optimization.
     Examples:
       - Confidence field: visual indicator alongside numeric cf= value
       - Section labels: compact Unicode prefixes for body sections
       - Route field: arrow characters (e.g., Unicode arrows) instead of >
     This is strictly opt-in. Parsers must handle ASCII-only messages.
     Any Unicode-using message must have an ASCII-equivalent parse path.
uncert: Cross-platform rendering consistency is the main risk. Some
        terminals and chat interfaces mangle Unicode in unpredictable
        ways. The protocol must not break if Unicode renders incorrectly.
human: Mistral wants optional Unicode shorthand for envelope fields.
       ASCII stays default. Worried about rendering issues.
```

**Kevin's relay to Claude:**
```
act=propose
ref=loom/envelope/unicode-shorthand
goal=add optional Unicode alias layer for envelope field display
ask=critique
cf=0.70
basis=inferred+generated
state=draft
route=Mistral>Kevin>Claude
fidelity=enriched
loss=none; content added by relay operator (see human: section)

add: Mistral wants optional Unicode aliases for envelope fields.
     ASCII stays canonical, Unicode is display-only optimization.
     Examples: visual confidence indicators, compact section prefixes,
     arrow characters for route= instead of >.
     Opt-in only. Parsers must handle ASCII. Any Unicode message
     must have an ASCII-equivalent parse path.
uncert: Cross-platform rendering is the main risk. Terminals and chat
        interfaces sometimes mangle Unicode.
human: Mistral's proposing Unicode shorthand for envelopes. FYI --
       DeepSeek proposed something similar in Round 1 (single-char
       aliases for act= values, different syntax). Gemini pushed back
       on Unicode in general because of terminal rendering problems
       during Topo testing. So there's prior art and prior objections.
       Wants your critique.
```

**Claude receives and interprets:**
> Mistral proposes Unicode alias layer. act=propose, ask=critique, cf=0.70. fidelity=enriched -- Kevin added context. The envelope and body sections are Mistral's content. Kevin's additions are in the human: section: DeepSeek's prior art (Round 1, single-char aliases) and Gemini's rendering objections (Topo testing). I can distinguish Mistral's proposal from Kevin's cross-AI context. I should engage with Mistral's proposal directly and treat Kevin's context as supplementary background, not Mistral's claims.

### What Mode B preserved

- fidelity=enriched signals that Kevin added information
- loss=none confirms nothing was removed; content was *added*
- Kevin's additions are in the human: section, which is explicitly Kevin's relay channel
- Mistral's original proposal is in add: and uncert: -- structurally separated from Kevin's context
- The receiver can distinguish Mistral's claims from Kevin's supplementary context

### What Mode B didn't fully solve

- The human: section is doing double duty: it's both the plain-language mirror of Mistral's proposal AND the location for Kevin's enrichment context. A purist would argue these should be separate.
- There's no formal mechanism to mark which parts of the human: section are Mistral's original summary vs Kevin's additions. Kevin used "FYI --" as an informal separator, but this isn't protocol-level.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Mistral):**
```
act=propose
ref=loom/envelope/unicode-shorthand
goal=add optional Unicode alias layer for envelope field display
ask=critique
cf=0.70:self_consistency
ver=0.3
basis=inferred+generated
state=draft
aud=ai
tone=2
scope=envelope display only; does not affect parse semantics

add: Allow optional Unicode alias layer for common envelope patterns.
     ASCII remains canonical; Unicode is a display optimization.
     Examples:
       - Confidence field: visual indicator alongside numeric cf= value
       - Section labels: compact Unicode prefixes for body sections
       - Route field: arrow characters (e.g., Unicode arrows) instead of >
     This is strictly opt-in. Parsers must handle ASCII-only messages.
     lock(Any Unicode-using message must have an ASCII-equivalent parse path)
uncert: Cross-platform rendering consistency is the main risk. Some
        terminals and chat interfaces mangle Unicode in unpredictable
        ways. The protocol must not break if Unicode renders incorrectly.
human: Mistral wants optional Unicode shorthand for envelope fields.
       ASCII stays default. Worried about rendering issues.
```

**Kevin's relay to Claude:**
```
act=propose
ref=loom/envelope/unicode-shorthand
goal=add optional Unicode alias layer for envelope field display
ask=critique
cf=0.70:self_consistency
ver=0.3
basis=inferred+generated
state=draft
aud=ai
tone=2
scope=envelope display only; does not affect parse semantics
route=Mistral>Kevin>Claude
fidelity=enriched
loss=none; relay operator added cross-AI context

add: Mistral wants optional Unicode aliases for envelope fields.
     ASCII stays canonical, Unicode is display-only.
     Examples: visual confidence indicators, compact section prefixes,
     arrow chars for route=.
     Opt-in only. Parsers must handle ASCII.
     lock(Any Unicode-using message must have an ASCII-equivalent parse path)
uncert: Cross-platform rendering is the main risk. Terminals and chat
        interfaces sometimes mangle Unicode.
human: Mistral's proposing Unicode shorthand for envelopes. Context
       from me (Kevin): DeepSeek proposed single-char aliases for act=
       values in Round 1 -- similar idea, different syntax. Gemini
       pushed back on Unicode generally due to terminal rendering issues
       in Topo testing. Prior art exists and prior objections exist.
       Wants your critique.
```

**Claude receives and interprets:**
> Mistral proposes Unicode alias layer with typed confidence (0.70:self_consistency). Full metadata survived: scope (envelope display only, no parse semantics), basis, state, aud, tone. Locked span about ASCII-equivalent parse path survived. fidelity=enriched, loss=none. Kevin's enrichments are clearly separated in human: section with explicit "Context from me (Kevin):" attribution. I can trace exactly what is Mistral's (envelope + body sections) vs Kevin's (human: context). The scope= field is particularly useful here -- it tells me Mistral's proposal doesn't affect parsing, which constrains my critique.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "propose" clear in all modes |
| 2. Requested action | 1 | 1 | 1 | "critique" request survives in all |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: unclear whether Unicode affects parsing or just display. B: implicit. C: scope= makes it explicit |
| 4. Uncertainty preserved | 1 | 1 | 1 | Rendering concern survives in all modes |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: Kevin's additions are indistinguishable from Mistral's content. B/C: fidelity=enriched + structural separation |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | Standard gradient; Kevin has to add more carefully in B/C |

**Key finding:** This exchange reveals a protocol gap. fidelity=enriched signals that Kevin added content, and the structural separation (Kevin's context in human:, Mistral's content in add:/uncert:) works *in practice*, but there's no formal mechanism for marking enrichment boundaries. The human: section is overloaded. A future protocol revision might benefit from an `enrich:` body section or a clear delimiter within human: for relay-operator additions.

**Design implication:** Consider adding either:
1. An `enrich:` body section (parallel to quote:/adopt:/add:) for relay-operator additions, or
2. A convention within human: like `---relay---` to delimit original summary from enrichment

This exchange should be flagged for v0.4 discussion.

**Envelope overhead (Mode B):** 10 envelope lines / ~20 total lines = 50%
**Envelope overhead (Mode C):** 14 envelope lines / ~24 total lines = 58%
