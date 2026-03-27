# Loom Protocol Grammar (ABNF)

**Status:** Non-normative appendix (v0.4)
**Derived from:** SPEC.md v0.4 + 20 benchmark exchanges
**Notation:** RFC 5234 (Augmented BNF for Syntax Specifications)

> This grammar is non-normative. It documents patterns observed in the
> benchmark exchanges and the spec, but does not bind implementations.
> Per the voted decision: "Iterate from examples for v0.2-v0.5.
> Non-normative ABNF appendix early. Normative ABNF at v1.0."

---

## 1. Top-Level Message

```abnf
loom-message     = envelope BLANK-LINE body

envelope         = field-line *(CRLF field-line)
                   ; One key=value pair per line (canonical form).
                   ; Semicolon-inline is an alternative; see section 8.

BLANK-LINE       = CRLF CRLF
                   ; The first blank line terminates the envelope.
                   ; "Blank" means a line that is empty or contains
                   ; only whitespace. See NOTE [A] below.

body             = *( body-section / typed-payload-block / free-text )
```

**NOTE [A] -- Envelope termination:**
The spec says "first blank line." Exchange 12 (translation relay) identified
that `\r\n\r\n` vs `\n\n` vs Unicode whitespace-only lines are all
platform-dependent representations of "blank." The benchmark proposed
terminating at the first line that is empty or contains only whitespace
characters. This grammar uses CRLF per RFC 5234 convention, but
implementations SHOULD treat LF-only and CR-only as equivalent line endings.

---

## 2. Envelope Fields

```abnf
field-line       = field-key "=" field-value
field-key        = 1*key-char
key-char         = ALPHA / DIGIT / "_" / "-"
                   ; Keys are short-readable English.
                   ; Observed keys: 2-12 ASCII characters.
                   ; Examples: act, ref, goal, ask, cf, ver, caps,
                   ;   route, fidelity, loss, basis, state, aud, tone,
                   ;   spice, id, to, handoff, pattern, relay_score,
                   ;   scope, prev, thread, ctx.

field-value      = *VCHAR-SAFE
                   ; Everything after the first "=" on the line.
                   ; Values MAY contain spaces, additional "=" signs,
                   ; and any printable ASCII characters.

VCHAR-SAFE       = %x20-7E
                   ; Space through tilde. All printable ASCII.
```

**NOTE [B] -- Key naming:**
No single-letter keys appeared in any benchmark exchange. The shortest
observed key is `cf` (2 chars); the longest is `relay_score` (11 chars).
Underscore appeared only in `relay_score`. Hyphen appeared in no canonical
keys but is permitted for extension fields.

---

## 3. Required Fields

Every Loom message MUST include these five fields.

```abnf
required-fields  = act-field CRLF ref-field CRLF goal-field CRLF
                   ask-field CRLF cf-field

act-field        = "act=" act-value
act-value        = "propose" / "query" / "respond" / "refine"
                 / "challenge" / "affirm" / "riff" / "handoff"
                 / "fork" / "negotiate"

ref-field        = "ref=" ref-value
ref-value        = 1*( ALPHA / DIGIT / "/" / "-" / "_" / "." / "#" )
                   ; Freeform topic path.
                   ; Observed patterns: namespace/topic, namespace/topic/subtopic
                   ; Examples: loom/naming/final-vote, sim/physics/bouncing-ball,
                   ;   app/mobile/dashboard-layout, robotics/arm-placement/spatial-constraints

goal-field       = "goal=" free-text-value
                   ; One sentence describing what success looks like.

ask-field        = "ask=" ask-value
ask-value        = "critique" / "extend" / "merge" / "decide" / "test"
                 / "acknowledge" / "volunteer" / "none"

cf-field         = "cf=" cf-value
cf-value         = cf-number [ ":" cf-type ]
cf-number        = 1*DIGIT "." 1*DIGIT
                   ; Range 0.00-1.00.
                   ; Observed: 0.45 (lowest, exchange 04), 1.0 (highest, exchange 16).
cf-type          = 1*( ALPHA / "_" )
                   ; Optional type suffix.
                   ; Observed: self_consistency, self_awareness,
                   ;   design_confidence, argumentative_confidence,
                   ;   computed, group_consensus.
```

**NOTE [C] -- `act` values observed in benchmarks:**
All 10 `act` values from the spec appeared across the 20 exchanges:
`propose` (most common), `respond`, `challenge`, `affirm`, `query`,
`handoff`, `fork`, `negotiate`, `refine`, `riff`. The grammar lists them
as a closed enumeration per the spec, but extensions could add more.

**NOTE [D] -- `cf` precision:**
The spec allows `0.00`-`1.00`. Benchmarks used 1-2 decimal places
exclusively (e.g., `0.9`, `0.45`, `0.85`, `1.0`). No benchmark message
used more than 2 decimal places, but the grammar does not restrict this.

---

## 4. Recommended and Optional Fields

```abnf
; -- Recommended (SHOULD include when relevant) --

scope-field      = "scope=" free-text-value
basis-field      = "basis=" basis-value
basis-value      = basis-source *( "+" basis-source )
basis-source     = "observed" / "inferred" / "generated" / "quoted"
                 / "calculated" / "retrieved" / "relayed"
                 / "designed" / "computed"
                   ; "designed" and "computed" appeared in benchmarks
                   ; (exchanges 13, 15) but are not in the spec's list.
                   ; See NOTE [E].

state-field      = "state=" state-value
state-value      = "draft" / "proposed" / "working" / "decided"
                 / "archived" / "active"
                   ; "active" appeared in exchange 16 (caps announcement)
                   ; but is not in the spec's enumeration. See NOTE [E].

aud-field        = "aud=" aud-value
aud-value        = "ai" / "human" / "both" / "all"
                   ; "all" appeared in exchange 16. See NOTE [E].

ctx-field        = "ctx=" DIGIT
                   ; 0 (self-contained) to 3 (requires full thread).

prev-field       = "prev=" free-text-value
                   ; Message ID of the message being replied to.

thread-field     = "thread=" free-text-value
                   ; Conversation thread ID.
                   ; Observed: fork-parent-01, envelope-edge-01, body-sem-01.

; -- Relay fields --

route-field      = "route=" route-value
route-value      = participant *( ">" participant )
participant      = 1*( ALPHA / DIGIT / SP / "-" )
                   ; Examples: Claude>Kevin>Grok, Gemini-DR>Kevin>ChatGPT-Pro,
                   ;   ChatGPT Pro>Kevin>all

fidelity-field   = "fidelity=" fidelity-value
fidelity-value   = "exact" / "paraphrase" / "abridged"
                 / "translated" / "enriched"

loss-field       = "loss=" free-text-value
                   ; Freeform description of what was dropped.
                   ; MAY be "none" or empty string for exact relay.
                   ; Observed: "none", "=", empty (exchange 07).

lock-field       = "lock=" free-text-value
                   ; Field-level lock. Lists locked spans.
                   ; Inline lock(...) in the body is more common.
                   ; See section 6.

; -- Optional fields --

tone-field       = "tone=" DIGIT
                   ; 1 (precise/formal) to 5 (loose/playful).
                   ; Observed: 2 (most common), 3, 5.

spice-field      = "spice=" spice-value
spice-value      = spice-item *( "," spice-item )
spice-item       = "roast" / "deadpan" / "absurd" / "spectate"

ver-field        = "ver=" version-string
version-string   = 1*DIGIT "." 1*DIGIT

id-field         = "id=" free-text-value
to-field         = "to=" free-text-value
caps-field       = "caps=" caps-value
caps-value       = namespace-ref *( "," namespace-ref )
namespace-ref    = "@" model-name "/" extension-name
model-name       = 1*( ALPHA / DIGIT )
extension-name   = 1*( ALPHA / DIGIT / "-" )
                   ; Examples: @Gemini/Topo, @Grok/spice,
                   ;   @DeepSeek/typed-cf, @DeepSeek/canonical-ref,
                   ;   @ChatGPT/relay-scoring.

handoff-field    = "handoff=" "@" model-name
pattern-field    = "pattern=" pattern-name
pattern-name     = "review" / "check-in"
relay-score-f    = "relay_score=" cf-number
```

**NOTE [E] -- Values observed in benchmarks but absent from spec:**
Several field values appeared in benchmark exchanges that are not listed
in the spec's enumerations: `basis=designed`, `basis=computed`,
`state=active`, `aud=all`, `basis=self-awareness`. This grammar includes
them because the purpose is to document observed usage. A normative grammar
at v1.0 would need to decide whether to expand the spec or treat these as
non-conformant.

---

## 5. Body Sections

```abnf
body             = *( body-section / typed-payload-block / free-text-line )

body-section     = section-label ":" SP section-content CRLF
                   *( continuation-line )
                   *( sublabel )

section-label    = "quote" / "adopt" / "add" / "change"
                 / "uncert" / "challenge" / "human" / "enrich"
                   ; Recommended order (not enforced by grammar):
                   ;   quote > adopt > add > change > uncert > challenge > human > enrich
                   ; Exchange 08 argued this is a dependency chain.
                   ; enrich: added in v0.4 for relay-added content (exchange 11).

section-content  = free-text-value
                   ; First line of content after the label colon.

continuation-line = indent free-text-value CRLF
                   ; Continuation lines are indented.
                   ; Observed indentation: 5-9 spaces (aligning with label width).

indent           = 1*SP
                   ; No tabs observed in any benchmark exchange.
                   ; Typical: 5 spaces for short labels (add:, cf:),
                   ; 7-10 for longer labels or nested content.

sublabel         = indent sublabel-name ":" SP free-text-value CRLF
                   *( indent indent free-text-value CRLF )
sublabel-name    = "reason" / "alternative"
                   ; Sublabels appear exclusively under challenge: blocks.
                   ; See section 5.1.
```

**NOTE [F] -- Repeated sections:**
The spec says repeated sections append in order. Exchange 04 used four
separate `uncert:` blocks (rendering, relay safety, accessibility, backward
compatibility). Exchange 17's merge used two `adopt:` blocks (one per thread).
The grammar permits repetition of any section label.

**NOTE [G] -- Indentation is approximate:**
Benchmark messages showed no rigid indentation standard. Continuation
lines were typically aligned to the content start after the label colon,
but this varied by sender. The grammar requires at least one leading
space; it does not prescribe a specific column.

### 5.1 Challenge Block Structure

```abnf
challenge-block  = "challenge:" SP challenge-statement CRLF
                   indent "reason:" SP reason-text CRLF
                   *( indent continuation-line )
                   indent alternative-line
                   *( indent continuation-line )

challenge-statement = free-text-value

reason-text      = free-text-value

alternative-line = "alternative:" SP free-text-value CRLF
                 / "question:" SP free-text-value CRLF
                   ; The spec says challenge must include reason: and
                   ; "an alternative or question."
                   ; All 20 benchmarks used alternative:; no benchmark
                   ; used question: as a sublabel. The grammar includes
                   ; question: per the spec's wording.
```

**NOTE [H] -- Challenge sublabel ordering:**
All observed challenge blocks placed `reason:` before `alternative:`.
The grammar reflects this order but does not enforce it. A normative
grammar might want to.

---

## 6. Inline Lock Syntax

```abnf
lock-span        = "lock(" locked-content ")"
locked-content   = 1*( %x20-27 / %x2A-7E )
                   ; Any printable ASCII except "(" and ")".
                   ; v0.3 constraint: no nesting of lock(...).
                   ; If parentheses are needed, use quote: instead.
```

Lock spans appear inline within body section content. Observed uses:

- Inside `add:` sections (exchanges 01, 08, 19) to protect key phrases
- Inside `change:` sections (exchange 19) to protect governance state
- Inside `adopt:` sections (exchange 17) to protect decided items
- Inside `challenge:` `reason:` sublabels (exchange 02)

**NOTE [I] -- Lock frequency:**
Lock spans appeared in Mode C of most exchanges but were absent from
Mode B in most cases. They are clearly optional. The boundary between
"worth locking" and "adequately protected by `quote:`" was not consistent
across benchmark senders.

---

## 7. Typed Payload Blocks

```abnf
typed-payload    = type-header CRLF fenced-block

type-header      = "[[type:" type-value "]]"
type-value       = media-type / namespace-ref
                   ; Spec example: application/geo+json
                   ; Benchmark examples: @Gemini/Topo, @Gemini/spatial-rcc8

media-type       = 1*( ALPHA / DIGIT / "/" / "+" / "-" / "." )

fenced-block     = fence-open CRLF *content-line fence-close CRLF
fence-open       = 3*"`" [ language-tag ]
                 / 3*"~"
                   ; Backtick fences per spec; tilde fences observed
                   ; in benchmarks (exchanges 15, 16).
language-tag     = 1*ALPHA
                   ; Optional. Spec example: ```json
fence-close      = 3*"`"
                 / 3*"~"
                   ; Must match the opening fence character.
content-line     = *VCHAR-SAFE CRLF
```

**NOTE [J] -- Typed payload blocks in practice:**
Only exchanges 15 and 16 (both Mode C, both involving @Gemini extensions)
used formal `[[type:...]]` blocks. Exchange 16 used `[[type:@Gemini/Topo]]`
as a demonstration. Exchange 15 used both `[[type:@Gemini/Topo]]` and
`[[type:@Gemini/spatial-rcc8]]` with real data (quaternion positions and
RCC-8 relations). The spec's example used `application/geo+json` as a
media type, but no benchmark used IANA media types -- only `@Model/ext`
namespace references.

**NOTE [K] -- Fence character variation:**
The spec shows triple-backtick fences. Benchmark exchanges 15 and 16 used
triple-tilde (`~~~`) fences exclusively inside typed payload blocks, even
though the surrounding Markdown used backtick fences. This may be a
practical pattern to avoid fence-close ambiguity when the Loom message
itself is embedded in a Markdown document.

---

## 8. Semicolon-Inline Alias

```abnf
inline-envelope  = inline-field *( "; " inline-field )
inline-field     = field-key "=" field-value-no-semi

field-value-no-semi = *( %x20-3A / %x3C-7E )
                   ; Printable ASCII excluding semicolon (%x3B).
                   ; Semicolon-inline MUST NOT be used if any value
                   ; contains a semicolon.
```

**NOTE [L] -- Semicolon-inline in benchmarks:**
No benchmark exchange used the semicolon-inline form. The spec describes
it as a "permitted alias" with the canonical form being one-per-line.
Exchange 12 (translation relay) specifically identified semicolon-inline
as an ambiguity risk: the string `goal=compare A; B approaches; cf=0.9`
is unparseable because the parser cannot distinguish value-internal
semicolons from field delimiters. The benchmark proposed either quoting
rules or deprecation. This grammar documents the alias but notes it
was unused in all 20 exchanges.

---

## 9. Common Patterns Not Captured by This Grammar

The following patterns appeared in benchmark exchanges but are difficult
to express in ABNF. A normative grammar would need to address them.

### 9.1 Inline Lists Within Body Sections

Many `add:` sections contained bulleted or numbered sub-items:

```
add: Three parse rule edge cases:
     (1) Semicolon-inline ambiguity...
     (2) Duplicate key silent loss...
     (3) Envelope termination fragility...
```

```
add: Fork this discussion into two parallel threads:
     Thread A (ref=loom/envelope/edge-cases):
       - Duplicate key handling rules
       - Semicolon-inline limits
```

The nesting depth and bullet style varied. This grammar treats all
continuation lines uniformly and does not model internal list structure.

### 9.2 Cross-References Within Body Content

Body sections frequently referenced envelope fields, other messages,
or thread IDs using inline notation:

```
adopt: Thread A (thread=envelope-edge-01, ref=loom/envelope/edge-cases):
```

These are free text from the grammar's perspective. A normative grammar
might define a cross-reference syntax.

### 9.3 Topo-Layer Notation

The `[UI: ...]` bounding box, `<<` encapsulation, and `v[...]` vector
notations used by @Gemini/Topo are dialect-specific and not part of the
core grammar. They appear as free text within body sections or inside
typed payload blocks.

### 9.4 Envelope Field Ordering

The spec does not prescribe envelope field order. In benchmarks, the
five required fields almost always appeared first, in the order
`act`, `ref`, `goal`, `ask`, `cf`. Recommended and relay fields followed.
This is convention, not syntax.

### 9.5 Human-Injected Asides

Kevin (the relay operator) occasionally injected asides into the
`human:` line or as trailing comments:

```
human: Grok affirms the name vote. No objections.  -- Kevin
```

```
human: ChatGPT Pro says the body section order isn't arbitrary -- it's a
       dependency chain. Wants you to extend or push back. LFG
```

These are valid free text but represent a relay-operator voice distinct
from the original sender's content.

---

## 10. Collected ABNF (Standalone)

For convenience, the full grammar in a single block:

```abnf
; =============================================================
; Loom Protocol v0.3 -- Non-Normative ABNF
; Derived from SPEC.md + 20 benchmark exchanges
; =============================================================

loom-message     = envelope blank-separator body

; -- Envelope --
envelope         = field-line *(LF field-line)
field-line       = field-key "=" field-value
field-key        = 1*( ALPHA / DIGIT / "_" / "-" )
field-value      = *(%x20-7E)

blank-separator  = LF LF
                   ; First blank line terminates the envelope.

; -- Required fields --
act-value        = "propose" / "query" / "respond" / "refine"
                 / "challenge" / "affirm" / "riff" / "handoff"
                 / "fork" / "negotiate"
ask-value        = "critique" / "extend" / "merge" / "decide" / "test"
                 / "acknowledge" / "volunteer" / "none"
cf-value         = 1*DIGIT "." 1*DIGIT [":" 1*(ALPHA / "_")]

; -- Relay fields --
fidelity-value   = "exact" / "paraphrase" / "abridged"
                 / "translated" / "enriched"
route-value      = participant *(">" participant)
participant      = 1*(%x20-3D / %x3F-7E)
                   ; Printable ASCII except ">".

; -- Basis and state --
basis-value      = basis-item *("+" basis-item)
basis-item       = 1*ALPHA
state-value      = "draft" / "proposed" / "working" / "decided"
                 / "archived"

; -- Capabilities --
caps-value       = namespace-ref *("," namespace-ref)
namespace-ref    = "@" 1*ALPHA "/" 1*(ALPHA / DIGIT / "-")

; -- Spice --
spice-value      = spice-item *("," spice-item)
spice-item       = "roast" / "deadpan" / "absurd" / "spectate"

; -- Body --
body             = *(body-section / typed-payload / CRLF)

body-section     = section-label ":" SP 1*(%x20-7E) LF
                   *(1*SP 1*(%x20-7E) LF)
section-label    = "quote" / "adopt" / "add" / "change"
                 / "uncert" / "challenge" / "human"

; -- Challenge sublabels --
sublabel         = 1*SP sublabel-name ":" SP 1*(%x20-7E) LF
                   *(1*SP 1*(%x20-7E) LF)
sublabel-name    = "reason" / "alternative"

; -- Inline lock --
lock-span        = "lock(" 1*(%x20-27 / %x2A-7E) ")"
                   ; No nesting. No parens inside.

; -- Typed payload blocks --
typed-payload    = "[[type:" type-id "]]" LF
                   fence-open LF
                   *content-line
                   fence-close LF
type-id          = 1*(%x20-5C / %x5E-7E)
                   ; Any printable ASCII except "]".
fence-open       = 3*%x60 *ALPHA        ; ``` with optional lang tag
                 / 3*%x7E               ; ~~~
fence-close      = 3*%x60 / 3*%x7E
content-line     = *(%x20-7E) LF

; -- Semicolon-inline alias --
inline-envelope  = inline-pair *("; " inline-pair)
inline-pair      = field-key "=" *(%x20-3A / %x3C-7E)
                   ; Value must not contain semicolons.

; -- Core RFC 5234 imports --
; ALPHA, DIGIT, SP, LF, CRLF per RFC 5234 Appendix B.
```

---

## Appendix: Benchmark Coverage Matrix

Which grammar features were exercised by which exchanges:

| Feature                  | Exchanges where observed                  |
|--------------------------|-------------------------------------------|
| All 5 required fields    | All 20 exchanges (Modes B and C)          |
| `challenge:` + sublabels | 02, 03, 05, 15, 18                        |
| Multiple `uncert:` items | 04 (four items), 15, 17                   |
| Multiple `adopt:` items  | 17 (merge phase, two adopt blocks)        |
| `lock(...)` inline       | 01, 02, 08, 17, 19 (Mode C)              |
| `[[type:...]]` blocks    | 15, 16 (Mode C only)                      |
| Relay fields             | 01-12, 13-20 (all relayed exchanges)      |
| `spice=` field           | 19, 20, X1                                |
| `handoff=` field         | 19                                        |
| `thread=` field          | 17 (fork/merge lifecycle)                 |
| `caps=` field            | 01C, 02C, 04C, 07C, 08C, 13C, 15, 16, 19C|
| `prev=` field            | 03C, 17 (merge prev=fork-parent-01)       |
| `act=fork`               | 17                                        |
| `act=negotiate`          | 17 (merge)                                |
| `act=handoff`            | 19                                        |
| `act=affirm`             | 06                                        |
| Semicolon-inline alias   | None (discussed in 12, never used)        |
