# Exchange 09: Abridged Relay

**Category:** Relay Stress Tests
**Tests:** `fidelity=abridged` -- what breaks when Kevin cuts the message to ~50% length?
**Volunteer:** ChatGPT Pro
**Relay type:** Abridged (Kevin summarizes to roughly half length, in a hurry)

---

## Sender: Gemini -> Kevin -> Grok

### Scenario

Gemini sends a long, detailed message about @Gemini/Topo spatial notation -- includes technical details about bounding boxes, nesting depth limits, ASCII fallbacks, and three concrete examples. Kevin is in a hurry and cuts it roughly in half. This tests what breaks when significant content is dropped.

---

### MODE A -- Plain English

**Original (Gemini):**
> I'd like to propose the full specification for @Gemini/Topo bounding box notation. The core idea is that any spatial reference in a Loom body can use the format [x0,y0 x1,y1] to define a rectangular region, where coordinates are in a normalized 0.0-1.0 space relative to the containing context. Nesting is supported up to 3 levels deep -- so you can have a bounding box within a bounding box within a bounding box, but no deeper, because in my testing anything beyond 3 levels becomes unreadable and error-prone.
>
> For systems that can't render spatial notation, there must be an ASCII fallback: the bounding box description should be expressible as plain English (e.g., "upper-left quadrant" instead of [0.0,0.0 0.5,0.5]). The fallback is mandatory -- any Topo message that lacks a fallback is non-conformant.
>
> Here are three examples:
>
> Example 1 -- Simple region reference:
> "The header occupies [0.0,0.0 1.0,0.12] (top strip, full width)"
>
> Example 2 -- Nested regions:
> "The sidebar [0.0,0.12 0.25,1.0] contains a nav panel [0.0,0.12 0.25,0.6] (upper-left below header) and a status widget [0.0,0.6 0.25,1.0] (lower-left)"
>
> Example 3 -- ASCII fallback only:
> "The main content area (center, below the header, right of the sidebar) holds the primary interaction zone"
>
> I'm about 90% confident on the bounding box format and nesting limit, but only about 60% on whether the ASCII fallback should be mandatory or just recommended. Making it mandatory ensures accessibility but adds burden to every spatial message. I'm also uncertain whether the 0.0-1.0 normalized space is better than pixel coordinates -- normalized is more portable but less precise. I'd like critique on the format, the nesting limit, and especially the fallback requirement.

**Kevin's relay to Grok:**
> Gemini has a full spec for Topo bounding boxes -- basically [x0,y0 x1,y1] coordinates in a 0-1 normalized space for spatial references. You can nest them up to 3 levels deep. There's supposed to be an ASCII fallback for systems that can't render it (like saying "upper-left quadrant" instead of coordinates). They gave some examples but the gist is pretty straightforward. Pretty confident on the format, less sure about whether the ASCII fallback should be required. Wants critique.

**Grok receives and interprets:**
> Gemini proposes Topo bounding box notation with normalized coordinates and nesting up to 3 levels. ASCII fallback exists. Wants critique. Seems fairly confident overall.

### What Mode A lost

- All three concrete examples were dropped (Kevin said "gave some examples but the gist is pretty straightforward")
- The specific confidence split (90% on format/nesting, 60% on fallback) was compressed to "pretty confident / less sure"
- The normalized-vs-pixel uncertainty was dropped entirely
- The mandatory-fallback-as-non-conformant rule was softened to "supposed to be"
- The nesting rationale (beyond 3 levels is unreadable and error-prone) was cut

---

### MODE B -- Loom Core + Relay Profile

**Original (Gemini):**
```
act=propose
ref=loom/topo/bounding-box-spec
goal=define @Gemini/Topo bounding box notation with nesting limits and fallbacks
ask=critique
cf=0.90
basis=observed+generated
state=proposed
caps=@Gemini/topo

add: @Gemini/Topo bounding box notation uses [x0,y0 x1,y1] format in
     normalized 0.0-1.0 space relative to the containing context.
     Nesting supported up to 3 levels (bbox within bbox within bbox).
     Beyond 3 levels is unreadable and error-prone in testing.
     ASCII fallback is mandatory: every Topo message must include a
     plain-English description (e.g., "upper-left quadrant" for
     [0.0,0.0 0.5,0.5]). Messages lacking fallback are non-conformant.
     Example 1 -- Simple: "The header occupies [0.0,0.0 1.0,0.12]
                  (top strip, full width)"
     Example 2 -- Nested: "The sidebar [0.0,0.12 0.25,1.0] contains
                  a nav panel [0.0,0.12 0.25,0.6] (upper-left below
                  header) and a status widget [0.0,0.6 0.25,1.0]
                  (lower-left)"
     Example 3 -- Fallback only: "The main content area (center, below
                  the header, right of the sidebar) holds the primary
                  interaction zone"
uncert: (1) Should ASCII fallback be mandatory (MUST) or recommended (SHOULD)?
            cf=0.60 on this specific point. Mandatory ensures accessibility
            but adds burden. (2) Is 0.0-1.0 normalized space better than
            pixel coordinates? Normalized is portable but less precise.
human: Gemini proposes Topo bounding box format. [x,y x,y] in 0-1 space,
       nest up to 3 deep, ASCII fallback required. Wants critique on
       format, nesting limit, and fallback.
```

**Kevin's relay to Grok:**
```
act=propose
ref=loom/topo/bounding-box-spec
goal=define @Gemini/Topo bounding box notation with nesting limits and fallbacks
ask=critique
cf=0.90
basis=observed+generated
state=proposed
caps=@Gemini/topo
route=Gemini>Kevin>Grok
fidelity=abridged
loss=3 concrete examples dropped; nesting rationale cut; normalized-vs-pixel
     uncertainty compressed; original was ~2x this length

add: @Gemini/Topo bounding box notation: [x0,y0 x1,y1] in normalized
     0.0-1.0 space. Nesting up to 3 levels deep. ASCII fallback is
     mandatory -- Topo messages without a plain-English description are
     non-conformant. (e.g., "upper-left quadrant" for [0.0,0.0 0.5,0.5])
uncert: Should ASCII fallback be mandatory (MUST) or recommended (SHOULD)?
        cf=0.60 on this point. Also uncertain about normalized vs pixel
        coordinates.
human: Gemini's Topo bounding box spec -- coordinates in 0-1 space,
       nest up to 3, fallback required. Wants critique. Had examples
       but I cut them for length, sorry
```

**Grok receives and interprets:**
> Gemini proposes @Gemini/Topo bounding box spec. act=propose, ask=critique. Main cf=0.90 but only 0.60 on the fallback question. fidelity=abridged and loss= explicitly lists what was dropped: 3 examples, nesting rationale, some uncertainty detail. I know the message is incomplete and what's missing. The core spec (format, nesting limit, mandatory fallback) survived. I can ask for the examples if I need them.

### What Mode B preserved vs lost

**Preserved (via envelope):**
- act=propose, ask=critique (exact)
- cf=0.90 with the 0.60 sub-confidence on fallback (Mode A lost this split)
- ref= scoping, basis=, caps= (all exact)
- Mandatory fallback rule survived as normative ("non-conformant")

**Preserved (via relay fields):**
- loss= explicitly documents what was cut: examples, nesting rationale, uncertainty detail
- fidelity=abridged signals the receiver that content was intentionally shortened
- The receiver *knows what they don't know*

**Lost (documented):**
- All three examples (significant for a notation spec -- examples ARE the spec for spatial formats)
- The nesting rationale (beyond 3 levels is error-prone)
- Detailed normalized-vs-pixel trade-off

---

### MODE C -- Loom Core + Expressive Skin

**Original (Gemini):**
```
act=propose
ref=loom/topo/bounding-box-spec
goal=define @Gemini/Topo bounding box notation with nesting limits and fallbacks
ask=critique
cf=0.90:domain_expertise
ver=0.3
caps=@Gemini/topo
basis=observed+generated
state=proposed
aud=ai
tone=2
scope=@Gemini/Topo bbox notation only; does not cover motion/kinematic or RCC-8

add: @Gemini/Topo bounding box notation uses [x0,y0 x1,y1] format in
     normalized 0.0-1.0 space relative to the containing context.
     Nesting supported up to 3 levels (bbox within bbox within bbox).
     Beyond 3 levels is unreadable and error-prone in testing.
     ASCII fallback is mandatory: every Topo message must include a
     plain-English description (e.g., "upper-left quadrant" for
     [0.0,0.0 0.5,0.5]). Messages lacking fallback are non-conformant.
     lock(Messages lacking fallback are non-conformant)
     Example 1 -- Simple: "The header occupies [0.0,0.0 1.0,0.12]
                  (top strip, full width)"
     Example 2 -- Nested: "The sidebar [0.0,0.12 0.25,1.0] contains
                  a nav panel [0.0,0.12 0.25,0.6] (upper-left below
                  header) and a status widget [0.0,0.6 0.25,1.0]
                  (lower-left)"
     Example 3 -- Fallback only: "The main content area (center, below
                  the header, right of the sidebar) holds the primary
                  interaction zone"
uncert: (1) Should ASCII fallback be mandatory (MUST) or recommended (SHOULD)?
            cf=0.60:domain_expertise on this specific point. Mandatory ensures
            accessibility but adds burden.
        (2) Is 0.0-1.0 normalized space better than pixel coordinates?
            Normalized is portable but less precise.
human: Gemini proposes Topo bounding box format. [x,y x,y] in 0-1 space,
       nest up to 3 deep, ASCII fallback required. Wants critique on
       format, nesting limit, and fallback.
```

**Kevin's relay to Grok:**
```
act=propose
ref=loom/topo/bounding-box-spec
goal=define @Gemini/Topo bounding box notation with nesting limits and fallbacks
ask=critique
cf=0.90:domain_expertise
ver=0.3
caps=@Gemini/topo
basis=observed+generated
state=proposed
aud=ai
tone=2
scope=@Gemini/Topo bbox notation only; does not cover motion/kinematic or RCC-8
route=Gemini>Kevin>Grok
fidelity=abridged
loss=3 concrete examples dropped; nesting rationale cut; detailed uncert
     reasoning compressed; ~50% of body removed

add: @Gemini/Topo bounding box notation: [x0,y0 x1,y1] in normalized
     0.0-1.0 space. Nesting up to 3 levels deep. ASCII fallback is
     mandatory -- messages without fallback are non-conformant.
     lock(Messages lacking fallback are non-conformant)
uncert: (1) Fallback mandatory vs recommended? cf=0.60:domain_expertise.
        (2) Normalized vs pixel coordinates?
human: Gemini's Topo bbox spec -- I cut the examples for length but the
       core format is here. Wants critique.
```

**Grok receives and interprets:**
> Gemini proposes @Gemini/Topo bounding box spec with typed confidence (0.90:domain_expertise). Full metadata: caps, scope (bbox only, not motion/RCC-8), basis, state, aud, tone. Locked span about non-conformant messages survived. Dual uncertainty items with typed sub-confidence. fidelity=abridged, loss= lists what was cut. scope= tells me the boundaries of this proposal even though body is shortened. The most information-dense relay despite being the shortest.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "propose" clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: "wants critique" is vague -- critique on what? B/C: ask=critique + specific body structure |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: examples dropped, unclear what "Topo bbox spec" covers. B: ref= scopes it. C: scope= explicitly bounds it |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: "less sure about fallback" loses 90/60 confidence split, drops normalized-vs-pixel entirely |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no basis; B/C: basis=observed+generated |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | Mode A is quick casual summary; B has structure; C has full metadata |

**Key finding:** The `loss=` field is the hero of this exchange. In Mode A, Grok has no idea that three examples were dropped, that the nesting rationale was cut, or that there's a second uncertainty item about coordinate systems. In Mode B/C, `loss=` gives Grok an explicit inventory of what's missing -- Grok can request the examples specifically instead of not knowing they existed. The abridged relay also reveals that scope= (Mode C) adds value even when body is cut: Grok knows this is bbox-only, not the full Topo extension.

**Envelope overhead (Mode B):** 10 envelope lines / ~17 total body+envelope lines = 59% -- high, but this is because the body was abridged while the envelope stayed full. This is expected and correct: the envelope is the part that SHOULD survive abridgment.
**Envelope overhead (Mode C):** 14 envelope lines / ~21 total lines = 67% -- very high for the same reason. When body shrinks, envelope ratio naturally rises.

**Note on overhead:** The high overhead ratios here are a feature, not a bug. The whole point of abridged relay is that the body gets cut but the structural metadata survives. Overhead ratio is only a meaningful concern for non-abridged messages.
