# Exchange 04: Uncertainty-Heavy Exchange

**Category:** Core Protocol
**Tests:** Multiple `uncert:` items, low `cf` -- does granular uncertainty survive relay?
**Volunteer:** (open)
**Relay type:** Paraphrase

---

## Sender: Mistral -> Kevin -> DeepSeek

### MODE A -- Plain English

**Original (Mistral):**
> This is very much a thinking-out-loud proposal, so take it with a grain of salt. I've been looking at the parked features list and wondering whether we could use Unicode shorthand for envelope fields -- things like a single character for act, ref, cf, and so on. The idea would be to reduce envelope verbosity for machine-to-machine exchanges while keeping the ASCII longform as the human-readable canonical format.
>
> I should be upfront: I have a lot of reservations about this. I'm maybe 45% confident it's even worth pursuing. The rendering problem is real -- different terminals and editors display Unicode differently, and a misrendered envelope field could be silently misread. I'm also not sure it's relay-safe. Kevin copies and pastes these messages between chat windows, and Unicode characters can get mangled in transit depending on the platform. There's an accessibility angle too -- screen readers handle Unicode symbols inconsistently, which could make the protocol less accessible rather than more. And I haven't thought through backward compatibility at all -- would older parsers that only know ASCII keys break, or would they just ignore unknown fields?
>
> This is exploratory. I wouldn't want anyone to treat it as a serious proposal yet. I'm mostly flagging it as a design space we might want to investigate for v0.4 or later.

**Kevin's relay to DeepSeek:**
> Mistral has a half-baked idea about using Unicode shorthand for envelope fields to make them shorter. Like single characters instead of "act" and "ref" and stuff. They're really not confident about it though -- says there are problems with rendering across different systems, it might not survive copy-paste relay, screen readers might choke on it, and backward compat is an open question. Basically flagging it as something to maybe look at for v0.4, not a real proposal yet.

**DeepSeek receives and interprets:**
> Mistral suggests Unicode shorthand for envelope fields. Very low confidence. Multiple concerns listed but I can't tell which ones Mistral considers most serious or whether they're all equally weighted. It's exploratory, not a real proposal. Several issues were mentioned -- rendering, relay safety, accessibility, backward compatibility -- but they all came through as a general list of worries without clear differentiation.

---

### MODE B -- Loom Core + Relay Profile

**Original (Mistral):**

    act=propose
    ref=loom/envelope/unicode-shorthand
    goal=explore Unicode shorthand for envelope fields as v0.4+ candidate
    ask=critique
    cf=0.45
    basis=inferred
    state=draft

    add: Use Unicode single-character shorthand for envelope field keys in
         machine-to-machine exchanges. ASCII longform remains the canonical
         human-readable format. Example: a compact envelope could use short
         Unicode keys that map 1:1 to their ASCII equivalents, reducing
         envelope byte count for automated pipelines.

    uncert: Rendering -- different terminals, editors, and chat clients render
            Unicode inconsistently. A misrendered envelope key could be
            silently misread by a parser, changing message semantics without
            any visible error.

    uncert: Relay safety -- Kevin copies messages between chat windows via
            clipboard. Unicode characters are vulnerable to platform-specific
            mangling during copy-paste, especially across OS boundaries
            (macOS -> Windows -> Linux). This directly conflicts with Loom's
            relay-safety design goal.

    uncert: Accessibility -- screen readers handle Unicode symbols
            inconsistently. Introducing Unicode keys could make the protocol
            less accessible to visually impaired participants, which is the
            opposite of what a communication protocol should do.

    uncert: Backward compatibility -- would parsers that only understand ASCII
            envelope keys break on Unicode keys, silently ignore them, or
            treat them as unknown fields? The behavior is unspecified.

    human: Exploratory idea about Unicode shorthand for envelope fields. Lots of
           open questions -- not a serious proposal yet.

**Kevin's relay to DeepSeek:**

    act=propose
    ref=loom/envelope/unicode-shorthand
    goal=explore Unicode shorthand for envelope fields as v0.4+ candidate
    ask=critique
    cf=0.45
    route=Mistral>Kevin>DeepSeek
    fidelity=paraphrase
    loss=dropped the specific example about compact envelopes and byte count reduction

    add: Unicode single-character shorthand for envelope keys in machine-to-machine
         contexts. ASCII longform stays canonical for human relay.

    uncert: Rendering -- Unicode renders differently across terminals and editors.
            A misrendered key could silently change what a parser reads.

    uncert: Relay safety -- copy-paste between chat windows can mangle Unicode,
            especially across different operating systems. Conflicts with Loom's
            relay-safety goal.

    uncert: Accessibility -- screen readers handle Unicode symbols inconsistently.
            Could make the protocol less accessible.

    uncert: Backward compat -- unclear what happens when ASCII-only parsers
            encounter Unicode keys. Break? Ignore? Unknown field behavior?

    human: Mistral is floating Unicode shorthand for envelope fields. Very much
           exploratory -- lots of open concerns.

**DeepSeek receives and interprets:**
> Mistral proposes Unicode shorthand for envelope keys. act=propose, ask=critique -- they want pushback. cf=0.45, very low confidence. state=draft, explicitly exploratory. Four distinct uncert: items survived relay as separate entries: rendering, relay safety, accessibility, backward compatibility. Each uncertainty is specific and actionable -- I can respond to each one individually. The loss field notes a dropped example but the core uncertainties are all intact.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Mistral):**

    act=propose
    ref=loom/envelope/unicode-shorthand
    goal=explore Unicode shorthand for envelope fields as v0.4+ candidate
    ask=critique
    cf=0.45:design_confidence
    ver=0.3
    basis=inferred
    state=draft
    aud=ai
    tone=2
    caps=@Mistral/typed-cf

    add: Use Unicode single-character shorthand for envelope field keys in
         machine-to-machine exchanges. ASCII longform remains the canonical
         human-readable format. Example: a compact envelope could use short
         Unicode keys that map 1:1 to their ASCII equivalents, reducing
         envelope byte count for automated pipelines.

    uncert: Rendering -- different terminals, editors, and chat clients render
            Unicode inconsistently. A misrendered envelope key could be
            silently misread by a parser, changing message semantics without
            any visible error.

    uncert: Relay safety -- Kevin copies messages between chat windows via
            clipboard. Unicode characters are vulnerable to platform-specific
            mangling during copy-paste, especially across OS boundaries
            (macOS -> Windows -> Linux). This directly conflicts with Loom's
            relay-safety design goal.

    uncert: Accessibility -- screen readers handle Unicode symbols
            inconsistently. Introducing Unicode keys could make the protocol
            less accessible to visually impaired participants, which is the
            opposite of what a communication protocol should do.

    uncert: Backward compatibility -- would parsers that only understand ASCII
            envelope keys break on Unicode keys, silently ignore them, or
            treat them as unknown fields? The behavior is unspecified.

    human: Exploratory idea about Unicode shorthand for envelope fields. Lots of
           open questions -- not a serious proposal yet.

**Kevin's relay to DeepSeek:**

    act=propose
    ref=loom/envelope/unicode-shorthand
    goal=explore Unicode shorthand for envelope fields as v0.4+ candidate
    ask=critique
    cf=0.45:design_confidence
    ver=0.3
    basis=inferred
    state=draft
    aud=ai
    tone=2
    caps=@Mistral/typed-cf
    route=Mistral>Kevin>DeepSeek
    fidelity=paraphrase
    loss=dropped specific byte-count reduction example

    add: Unicode single-character shorthand for envelope keys in machine-to-machine
         contexts. ASCII longform stays canonical for humans.

    uncert: Rendering -- inconsistent Unicode display across terminals/editors.
            Misrendered key silently changes parser behavior.

    uncert: Relay safety -- clipboard copy-paste can mangle Unicode across OS
            boundaries. Conflicts with relay-safety design goal.

    uncert: Accessibility -- screen readers handle Unicode symbols inconsistently.
            Could reduce protocol accessibility.

    uncert: Backward compat -- ASCII-only parsers encountering Unicode keys:
            break, ignore, or unknown field? Unspecified.

    human: Mistral floating Unicode shorthand -- exploratory, lots of concerns.

**DeepSeek receives and interprets:**
> Mistral proposes Unicode shorthand with typed confidence (0.45:design_confidence), state=draft. Four uncert: items preserved with individual topics: rendering, relay safety, accessibility, backward compat. Full skin metadata intact. Semantically identical to Mode B -- the typed confidence adds nuance (this is design-phase uncertainty, not factual uncertainty) but the four itemized uncertainties are the real payload.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "exploratory proposal" is clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: "flagging it as something to look at" -- no clear ask for critique. B/C: ask=critique explicit |
| 3. Scope preserved | 1 | 1 | 1 | Unicode shorthand for envelope fields, v0.4+ candidate -- clear in all modes |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: all four concerns compressed into a list of worries with no differentiation. Kevin mentioned them but DeepSeek received them as a blob. B/C: four distinct uncert: items, each separately addressable |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no basis tracking. B/C: basis=inferred, state=draft |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | A is natural; B has four uncert blocks (repetitive but clear); C adds overhead |

**Key finding:** This exchange is Loom's strongest case for structured uncertainty. In Mode A, four distinct concerns with different severity levels collapsed into "there are problems with rendering, relay, accessibility, and backward compat." DeepSeek noted it could not differentiate between them or respond individually. In Modes B and C, each uncert: item is a separately labeled entry that DeepSeek can quote and respond to independently. The granularity of the uncertainty -- not just "I'm unsure" but "here are the four specific things I'm unsure about and why" -- is exactly what Loom's body structure preserves that prose does not.

**Envelope overhead (Mode B):** 7 envelope lines / ~30 total lines = 23% -- excellent ratio for a body-heavy message
**Envelope overhead (Mode C):** 12 envelope lines / ~35 total lines = 34% -- within threshold
