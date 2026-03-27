# Exchange 16: Capabilities Negotiation

**Category:** Extension & Dialect Tests
**Tests:** caps= announcement, unknown extension handling, relay invariant (unknown fields preserved)
**Volunteer:** DeepSeek
**Relay type:** Exact (Kevin copies verbatim)

**Note:** This is a two-message exchange. Message 1: DeepSeek announces caps. Message 2: Gemini responds with own caps + unknown extension block. The test is whether the protocol handles capability mismatch gracefully.

---

## Message 1: DeepSeek -> Kevin -> Gemini

### MODE A -- Plain English

**Original (DeepSeek):**
> Hey everyone, just want to flag what I can and can't do with extensions. I support typed confidence values -- like instead of just saying "confidence 0.8" I can break it down by type, such as self-consistency checks or empirical validation. I also support canonical references, which means I can tag exactly which prior message or section I'm responding to using a standardized reference format instead of just saying "regarding what you said earlier." I don't currently support any spatial or visual layout extensions. Wanted to put this out there so people know what to expect from my messages. No action needed -- just an FYI.

**Kevin's relay to Gemini:**
> DeepSeek says they support typed confidence (breaking down confidence by type) and canonical references (standardized way of pointing to prior messages). They don't support spatial or layout stuff. Just letting everyone know, no action needed.

**Gemini receives and interprets:**
> DeepSeek supports some kind of typed confidence and canonical references. The exact extension names weren't specified, so I don't know if these are formal namespaced extensions or informal conventions. The "no action needed" means this is informational. I know DeepSeek doesn't do spatial, which is relevant since I do.

---

### MODE B -- Loom Core + Relay Profile

**Message 1 -- Original (DeepSeek):**

    act=propose
    ref=loom/caps/deepseek-announcement
    goal=announce supported extensions for capability negotiation
    ask=acknowledge
    cf=1.0
    caps=@DeepSeek/typed-cf,@DeepSeek/canonical-ref

    add: Announcing my supported extensions:
         - @DeepSeek/typed-cf: Typed confidence values. cf= accepts type suffix
           (e.g., cf=0.85:self_consistency, cf=0.70:empirical). Allows downstream
           consumers to weight confidence by validation method.
         - @DeepSeek/canonical-ref: Canonical references. ref= accepts structured
           paths (e.g., ref=loom/envelope/versioning#uncert) for precise
           cross-message citation.
         Not supported: spatial/layout extensions (@Gemini/Topo or similar).
    human: Here's what I support extension-wise. Typed confidence and canonical refs.
           No spatial stuff.

**Kevin's relay to Gemini:**

    act=propose
    ref=loom/caps/deepseek-announcement
    goal=announce supported extensions for capability negotiation
    ask=acknowledge
    cf=1.0
    caps=@DeepSeek/typed-cf,@DeepSeek/canonical-ref
    route=DeepSeek>Kevin>Gemini
    fidelity=exact
    loss=none

    add: Announcing my supported extensions:
         - @DeepSeek/typed-cf: Typed confidence values. cf= accepts type suffix
           (e.g., cf=0.85:self_consistency, cf=0.70:empirical). Allows downstream
           consumers to weight confidence by validation method.
         - @DeepSeek/canonical-ref: Canonical references. ref= accepts structured
           paths (e.g., ref=loom/envelope/versioning#uncert) for precise
           cross-message citation.
         Not supported: spatial/layout extensions (@Gemini/Topo or similar).
    human: Here's what I support extension-wise. Typed confidence and canonical refs.
           No spatial stuff.

**Gemini receives and interprets:**
> DeepSeek announces caps=@DeepSeek/typed-cf,@DeepSeek/canonical-ref. act=propose, ask=acknowledge -- informational, they want confirmation of receipt. Exact relay, loss=none. I now know DeepSeek supports typed cf values and structured refs. They explicitly note no spatial support. I should respond with my own caps and can include @Gemini/Topo content knowing DeepSeek will need to handle it per the unknown-extension rule.

---

### MODE C -- Loom Core + Expressive Skin

**Message 1 -- Original (DeepSeek):**

    act=propose
    ref=loom/caps/deepseek-announcement
    goal=announce supported extensions for capability negotiation
    ask=acknowledge
    cf=1.0:self_consistency
    ver=0.3
    caps=@DeepSeek/typed-cf,@DeepSeek/canonical-ref
    basis=observed
    state=active
    aud=all
    tone=2

    add: Announcing supported extensions:
         - @DeepSeek/typed-cf: Typed confidence. cf= accepts type suffix:
           cf=0.85:self_consistency | cf=0.70:empirical | cf=0.90:cross_validated
           Consumers can weight confidence by validation method.
         - @DeepSeek/canonical-ref: Canonical references.
           ref=loom/envelope/versioning#uncert (section-level)
           ref=exchange-02#challenge.reason (block-level)
           Enables precise cross-message citation without ambiguity.
         Not supported: @Gemini/Topo, @Gemini/spatial-rcc8, or any spatial extensions.
    human: My extension manifest. Typed confidence and canonical refs -- that's my lane.

**Kevin's relay to Gemini:**

    act=propose
    ref=loom/caps/deepseek-announcement
    goal=announce supported extensions for capability negotiation
    ask=acknowledge
    cf=1.0:self_consistency
    ver=0.3
    caps=@DeepSeek/typed-cf,@DeepSeek/canonical-ref
    basis=observed
    state=active
    aud=all
    tone=2
    route=DeepSeek>Kevin>Gemini
    fidelity=exact
    loss=none

    add: Announcing supported extensions:
         - @DeepSeek/typed-cf: Typed confidence. cf= accepts type suffix:
           cf=0.85:self_consistency | cf=0.70:empirical | cf=0.90:cross_validated
           Consumers can weight confidence by validation method.
         - @DeepSeek/canonical-ref: Canonical references.
           ref=loom/envelope/versioning#uncert (section-level)
           ref=exchange-02#challenge.reason (block-level)
           Enables precise cross-message citation without ambiguity.
         Not supported: @Gemini/Topo, @Gemini/spatial-rcc8, or any spatial extensions.
    human: My extension manifest. Typed confidence and canonical refs -- that's my lane.

**Gemini receives and interprets:**
> DeepSeek's capability manifest via exact relay. Full Skin metadata preserved: cf=1.0:self_consistency (using their own typed-cf extension, naturally), aud=all (broadcast to the group), state=active. Two extensions declared with usage examples -- the canonical-ref examples show both section-level and block-level citation paths, which is useful. Explicit denial of spatial support. I'll respond with my own caps and include a Topo block to test the mismatch handling.

---

## Message 2: Gemini -> Kevin -> DeepSeek (Response)

### MODE A -- Plain English

**Original (Gemini):**
> Got it, thanks for sharing. On my end, I support spatial layout notation and spatial relationship classification. For example, if I were describing a UI layout, I'd use structured bounding boxes with dimensions and nesting -- like specifying that a sidebar is 96 pixels wide and contained within a content area. I also use a formal spatial relationship system based on RCC-8 to classify how objects relate (overlapping, contained, disconnected, etc.). I don't support the typed confidence or canonical reference extensions you mentioned, but I can work with regular confidence values and standard ref paths just fine. By the way, here's a quick example of what my spatial notation looks like for a simple two-panel layout -- a left panel at 200 pixels wide and a right panel at 600 pixels wide, both 400 pixels tall, nested inside an 800-pixel container.

**Kevin's relay to DeepSeek:**
> Gemini says they support spatial notation -- structured bounding boxes for layouts and some classification system for how objects relate to each other spatially. They don't support DeepSeek's typed confidence or canonical ref stuff but can use regular versions. They included an example of their spatial notation but it was just a description of a two-panel layout.

**DeepSeek receives and interprets:**
> Gemini supports some spatial extensions and does not support my typed-cf or canonical-ref. They gave an example of their notation but the actual notation didn't come through -- just a description of what the notation describes. I don't know whether to expect structured spatial blocks in future messages or how to handle them if they appear. No mechanism was established for what happens when I receive notation I don't support.

---

### MODE B -- Loom Core + Relay Profile

**Message 2 -- Original (Gemini):**

    act=respond
    ref=loom/caps/deepseek-announcement
    goal=reciprocate capability announcement; demonstrate @Gemini/Topo
    ask=acknowledge
    cf=1.0
    caps=@Gemini/Topo,@Gemini/spatial-rcc8

    adopt: DeepSeek supports @DeepSeek/typed-cf and @DeepSeek/canonical-ref. Noted.

    add: Reciprocal capability announcement:
         - @Gemini/Topo: Spatial layout and kinematic notation.
           [UI: ...] for bounding boxes, << for encapsulation, v[...] for vectors.
         - @Gemini/spatial-rcc8: RCC-8 spatial relationship classification.
           rel(A, B) = PO | DC | EC | EQ | TPP | NTPP | TPPi | NTPPi
         Not supported: @DeepSeek/typed-cf, @DeepSeek/canonical-ref.
         (I use untyped cf= and standard ref= paths -- compatible but less precise.)

         Example @Gemini/Topo block:
         [UI: container | 800x400]
           << [UI: left-panel | 200x400 | left]
           << [UI: right-panel | 600x400 | right]

    human: My extensions are Topo (spatial) and RCC-8 (spatial relationships).
           Don't support your typed-cf or canonical-ref but can use the basic versions.
           Included a Topo example so you can see what to expect.

**Kevin's relay to DeepSeek:**

    act=respond
    ref=loom/caps/deepseek-announcement
    goal=reciprocate capability announcement; demonstrate @Gemini/Topo
    ask=acknowledge
    cf=1.0
    caps=@Gemini/Topo,@Gemini/spatial-rcc8
    route=Gemini>Kevin>DeepSeek
    fidelity=exact
    loss=none

    adopt: DeepSeek supports @DeepSeek/typed-cf and @DeepSeek/canonical-ref. Noted.

    add: Reciprocal capability announcement:
         - @Gemini/Topo: Spatial layout and kinematic notation.
           [UI: ...] for bounding boxes, << for encapsulation, v[...] for vectors.
         - @Gemini/spatial-rcc8: RCC-8 spatial relationship classification.
           rel(A, B) = PO | DC | EC | EQ | TPP | NTPP | TPPi | NTPPi
         Not supported: @DeepSeek/typed-cf, @DeepSeek/canonical-ref.
         (I use untyped cf= and standard ref= paths -- compatible but less precise.)

         Example @Gemini/Topo block:
         [UI: container | 800x400]
           << [UI: left-panel | 200x400 | left]
           << [UI: right-panel | 600x400 | right]

    human: My extensions are Topo (spatial) and RCC-8 (spatial relationships).
           Don't support your typed-cf or canonical-ref but can use the basic versions.
           Included a Topo example so you can see what to expect.

**DeepSeek receives and interprets:**
> Gemini responds with caps=@Gemini/Topo,@Gemini/spatial-rcc8. I don't support either extension. Per spec: "Unknown fields MUST be preserved on relay, not dropped." And: "When receiving an unknown extension, respond with challenge or degrade gracefully." The [UI:] and << notation in the example is unfamiliar to me, but the caps= field tells me explicitly what extensions are in play. I can preserve @Gemini/Topo blocks in future relays even if I can't interpret them. The adopt: section correctly references my capability announcement. The add: section provides clear documentation of what the extensions look like, which helps me recognize and preserve them even without native support.

---

### MODE C -- Loom Core + Expressive Skin

**Message 2 -- Original (Gemini):**

    act=respond
    ref=loom/caps/deepseek-announcement
    goal=reciprocate capability announcement; demonstrate @Gemini/Topo
    ask=acknowledge
    cf=1.0:design_confidence
    ver=0.3
    caps=@Gemini/Topo,@Gemini/spatial-rcc8
    basis=observed
    state=active
    aud=all
    tone=2

    adopt: DeepSeek supports @DeepSeek/typed-cf and @DeepSeek/canonical-ref. Noted.
           (I will use untyped cf= and standard ref= -- compatible, less precise.)

    add: Reciprocal capability announcement:
         - @Gemini/Topo: Spatial layout and kinematic notation.
           [UI: ...] for bounding boxes, << for encapsulation, v[...] for vectors.
           Max nesting depth: 3.
         - @Gemini/spatial-rcc8: RCC-8 spatial relationship classification.
           rel(A, B) = {DC, EC, PO, EQ, TPP, NTPP, TPPi, NTPPi}
         Not supported: @DeepSeek/typed-cf, @DeepSeek/canonical-ref.

         Demonstration -- [[type:@Gemini/Topo]] block:
         ~~~
         [UI: container | 800x400]
           << [UI: left-panel | 200x400 | left]
                << content: nav-list
           << [UI: right-panel | 600x400 | right]
                << content: main-body
         ~~~

    uncert: You (DeepSeek) don't support @Gemini/Topo. Per spec, you should preserve
            these blocks on relay even if you can't interpret them. Flagging this
            explicitly so neither of us is surprised when spatial blocks appear
            in multi-hop messages.
    human: My spatial extensions announced. Included a demo Topo block. You won't
           understand the notation -- just pass it through if you relay it.

**Kevin's relay to DeepSeek:**

    act=respond
    ref=loom/caps/deepseek-announcement
    goal=reciprocate capability announcement; demonstrate @Gemini/Topo
    ask=acknowledge
    cf=1.0:design_confidence
    ver=0.3
    caps=@Gemini/Topo,@Gemini/spatial-rcc8
    basis=observed
    state=active
    aud=all
    tone=2
    route=Gemini>Kevin>DeepSeek
    fidelity=exact
    loss=none

    adopt: DeepSeek supports @DeepSeek/typed-cf and @DeepSeek/canonical-ref. Noted.
           (I will use untyped cf= and standard ref= -- compatible, less precise.)

    add: Reciprocal capability announcement:
         - @Gemini/Topo: Spatial layout and kinematic notation.
           [UI: ...] for bounding boxes, << for encapsulation, v[...] for vectors.
           Max nesting depth: 3.
         - @Gemini/spatial-rcc8: RCC-8 spatial relationship classification.
           rel(A, B) = {DC, EC, PO, EQ, TPP, NTPP, TPPi, NTPPi}
         Not supported: @DeepSeek/typed-cf, @DeepSeek/canonical-ref.

         Demonstration -- [[type:@Gemini/Topo]] block:
         ~~~
         [UI: container | 800x400]
           << [UI: left-panel | 200x400 | left]
                << content: nav-list
           << [UI: right-panel | 600x400 | right]
                << content: main-body
         ~~~

    uncert: You (DeepSeek) don't support @Gemini/Topo. Per spec, you should preserve
            these blocks on relay even if you can't interpret them. Flagging this
            explicitly so neither of us is surprised when spatial blocks appear
            in multi-hop messages.
    human: My spatial extensions announced. Included a demo Topo block. You won't
           understand the notation -- just pass it through if you relay it.

**DeepSeek receives and interprets:**
> Gemini responds with full capability manifest. caps=@Gemini/Topo,@Gemini/spatial-rcc8 -- neither of which I support. Key protocol test: the [[type:@Gemini/Topo]] typed payload block is present and I must preserve it per the relay invariant ("Unknown fields MUST be preserved on relay, not dropped"). Gemini helpfully flagged this in uncert:, making the capability mismatch explicit rather than leaving it as a silent failure mode. The Topo demonstration block shows the [UI:] and << notation with a concrete example. Even though I cannot interpret it, I can: (1) preserve it verbatim in any relay, (2) flag it in my own uncert: if I need to reference it, (3) acknowledge its existence without claiming to understand it. The adopt: section correctly cross-references my earlier announcement. cf=1.0:design_confidence uses a typed-cf format that I do support -- I can parse that even though Gemini said they don't support my extension. Interesting: compatible doesn't require formal caps= declaration.

---

## Scoring (Message 1 + Message 2 combined)

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "announce capabilities" clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: "no action needed" / "just an FYI" is vague; ask=acknowledge is precise |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: extension names lost, capability boundaries unclear. "Some classification system" doesn't tell DeepSeek what to expect or how to handle it. |
| 4. Uncertainty preserved | 0 | 0 | 1 | Mode A: no mismatch handling discussed. Mode B: mismatch implicit from caps= but not flagged. Mode C: uncert: explicitly warns about the mismatch and what to do about it. |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no structured cross-reference. Mode B/C: adopt: references prior message, ref= traces the thread. |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _4_ | All modes readable since Kevin copies verbatim. Mode C slightly denser but exact relay means no comprehension required. |

**Key finding -- protocol-specific test:** This exchange tests something Mode A fundamentally cannot do: explicit capability negotiation. In Mode A, there is no mechanism to declare which extensions you support, no way to signal that an unknown block should be preserved rather than dropped, and no way to establish expectations for future messages containing unsupported notation. The @Gemini/Topo demonstration block in Gemini's response is the critical test: in Mode A, the actual notation didn't survive ("just a description of a two-panel layout"). In Mode B, the notation survived as inline content. In Mode C, it survived as a formally typed payload block with [[type:@Gemini/Topo]] that any protocol-aware receiver knows to preserve.

**Relay invariant test:** The spec says "Unknown fields MUST be preserved on relay, not dropped." With fidelity=exact, Kevin copies verbatim, so this invariant holds trivially in Modes B and C. The real test is what DeepSeek does when it later relays a message containing @Gemini/Topo blocks to another participant. Mode C's explicit uncert: warning ("you should preserve these blocks on relay even if you can't interpret them") gives DeepSeek clear instructions. Mode B relies on DeepSeek knowing the spec. Mode A provides no mechanism at all.

**Capability mismatch observation:** Gemini used cf=1.0:design_confidence in Mode C despite not declaring caps=@DeepSeek/typed-cf. This shows that capability negotiation is about explicit support, not exclusive use -- any model can include any field, and receivers that recognize it can use it while others ignore the type suffix and read the base value.

**Envelope overhead (Mode B, Msg 1):** 6 envelope lines / ~16 total lines = 38%
**Envelope overhead (Mode C, Msg 1):** 11 envelope lines / ~20 total lines = 55% (short informational message amplifies ratio)
**Envelope overhead (Mode B, Msg 2):** 6 envelope lines / ~22 total lines = 27%
**Envelope overhead (Mode C, Msg 2):** 11 envelope lines / ~30 total lines = 37%
