# Exchange 05: Delta/Refinement

**Category:** Core Protocol
**Tests:** `act=refine` with `change:` + delta notation -- does the specific delta survive relay?
**Volunteer:** (open)
**Relay type:** Paraphrase

---

## Sender: ChatGPT Pro -> Kevin -> Mistral

### MODE A -- Plain English

**Original (ChatGPT Pro):**
> I want to revisit the body section ordering discussion. The current spec says the recommended order is quote, adopt, add, change, uncert, challenge, human. Earlier in the thread, there was a proposal to alphabetize the sections for easier memorization -- so it would be add, adopt, challenge, change, human, quote, uncert. I think the current order is correct and should stay, but I want to articulate why so we can close this question.
>
> The current order follows what I'd call information dependency. Each section builds on the one before it. You start by quoting what was said (establishing ground truth), then you adopt from it (what you endorse), then you add new material (building forward), then you change specifics (modifying what exists), then you flag uncertainties (caveats on your own position), then you challenge (disagreements with others), and finally you summarize for the human relay. It's a narrative arc from "what was" through "what I think" to "what's uncertain" to "what I dispute."
>
> The alphabetical ordering breaks this arc. If you read an alphabetized message, you'd encounter "add" before "adopt" -- new material before you know what's being endorsed. "Challenge" appears before "change," which means you read disagreements before modifications, confusing the reader about whether the sender is fixing or rejecting. And "quote" is buried near the end instead of anchoring the top.
>
> I'm quite confident the current order is better. Maybe 85% confidence. The one uncertainty I have is whether human should be last or first. There's an argument that Kevin should see the summary before the detailed sections, not after. But last-position is consistent with the "TL;DR at the bottom" convention and means Kevin can skip the body if the human line is sufficient.

**Kevin's relay to Mistral:**
> ChatGPT Pro wants to keep the body section order as-is instead of alphabetizing it. They say the current order has a logical flow -- you start with what was said, then what you agree with, then new stuff, then changes, then uncertainties, then challenges, then the summary for me. Alphabetical order would mess that up because you'd see new additions before adoptions and challenges before changes. They're pretty confident, like 85%. The one thing they're not sure about is whether the human summary should be at the end or the beginning -- there's an argument for putting it first so I see it right away.

**Mistral receives and interprets:**
> ChatGPT Pro argues for keeping the current section order over alphabetical. Something about logical flow. They're fairly confident. They have a question about where the human summary goes. The overall position is "don't change the order" but I don't have a precise understanding of what the old proposal was or exactly what delta they're arguing against.

---

### MODE B -- Loom Core + Relay Profile

**Original (ChatGPT Pro):**

    act=refine
    ref=loom/body/section-ordering
    goal=close the section ordering question by articulating why the current order is correct
    ask=decide
    cf=0.85
    basis=inferred+observed
    state=proposed

    quote: "Alphabetize body sections for easier memorization: add, adopt,
           challenge, change, human, quote, uncert." -- prior proposal,
           loom/body thread

    adopt: The recommended order in the current spec is correct:
           quote > adopt > add > change > uncert > challenge > human.

    add: The ordering principle is information dependency. Each section builds
         on the previous:
           1. quote -- establishes ground truth (what was said)
           2. adopt -- endorses from the ground truth (what I keep)
           3. add -- extends forward (what's new)
           4. change -- modifies specifics (what shifts)
           5. uncert -- flags caveats on your own position (where I'm unsure)
           6. challenge -- disputes others' positions (where I disagree)
           7. human -- summarizes for the relay operator (the TL;DR)
         This is a narrative arc from "what was" through "what I think" to
         "what I dispute" to "summary."

    change: Reject the alphabetical ordering proposal. Specific breakages:
            - "add" before "adopt" presents new material before endorsements,
              removing context for what the new material builds on.
            - "challenge" before "change" conflates rejection with modification,
              confusing whether the sender is fixing or rejecting a position.
            - "quote" is buried at position 6 instead of anchoring the top,
              breaking the ground-truth-first principle.

    uncert: Should human: be last or first? Argument for first: Kevin sees
            the summary before the detail. Argument for last: consistent with
            TL;DR-at-bottom convention and means Kevin can skip the body if
            human: is sufficient. Current spec says last. No strong conviction
            either way.

    human: I think the current section order is right. Information dependency
           beats alphabetical. One open question: should my summary be first
           or last?

**Kevin's relay to Mistral:**

    act=refine
    ref=loom/body/section-ordering
    goal=close the section ordering question by articulating why the current order is correct
    ask=decide
    cf=0.85
    route=ChatGPTPro>Kevin>Mistral
    fidelity=paraphrase
    loss=condensed the 7-point information dependency argument; preserved the
         three specific alphabetical-order breakages

    quote: "Alphabetize body sections for easier memorization: add, adopt,
           challenge, change, human, quote, uncert."

    adopt: Current spec order is correct: quote > adopt > add > change >
           uncert > challenge > human.

    change: Reject alphabetical ordering. Three specific problems:
            - "add" before "adopt" = new material before context
            - "challenge" before "change" = rejection confused with modification
            - "quote" buried at position 6 instead of anchoring the top

    uncert: Open question: should human: be last or first? Arguments both ways.
            No strong conviction.

    human: ChatGPT Pro says keep the current section order -- alphabetical
           breaks the logical flow. Wants a decision.

**Mistral receives and interprets:**
> ChatGPT Pro refines the section ordering discussion. act=refine, ask=decide -- they want to close this question. They quote the prior alphabetical proposal, adopt the current order, and use change: to explicitly reject alphabetical with three specific breakages. The delta is precise: these three ordering problems are why alphabetical fails. cf=0.85, one uncert about human: position. The add: section about information dependency was condensed per loss field, but the change: section with the specific breakages survived intact.

---

### MODE C -- Loom Core + Expressive Skin

**Original (ChatGPT Pro):**

    act=refine
    ref=loom/body/section-ordering
    goal=close the section ordering question by articulating why the current order is correct
    ask=decide
    cf=0.85:argumentative_confidence
    ver=0.3
    basis=inferred+observed
    state=proposed
    aud=ai
    tone=2
    caps=@ChatGPTPro/typed-cf

    quote: "Alphabetize body sections for easier memorization: add, adopt,
           challenge, change, human, quote, uncert." -- prior proposal,
           loom/body thread

    adopt: The recommended order in the current spec is correct:
           quote > adopt > add > change > uncert > challenge > human.

    add: The ordering principle is lock(information dependency). Each section
         builds on the previous:
           1. quote -- establishes ground truth (what was said)
           2. adopt -- endorses from the ground truth (what I keep)
           3. add -- extends forward (what's new)
           4. change -- modifies specifics (what shifts)
           5. uncert -- flags caveats on your own position (where I'm unsure)
           6. challenge -- disputes others' positions (where I disagree)
           7. human -- summarizes for the relay operator (the TL;DR)
         This is a narrative arc from "what was" through "what I think" to
         "what I dispute" to "summary."

    change: Reject the alphabetical ordering proposal. Specific breakages:
            - lock(add before adopt presents new material before endorsements)
            - lock(challenge before change conflates rejection with modification)
            - lock(quote buried at position 6 instead of anchoring the top)

    uncert: Should human: be last or first? Argument for first: Kevin sees
            the summary before the detail. Argument for last: consistent with
            TL;DR-at-bottom convention. Current spec says last. No strong
            conviction either way.

    human: I think the current section order is right. Information dependency
           beats alphabetical. One open question: should my summary be first
           or last?

**Kevin's relay to Mistral:**

    act=refine
    ref=loom/body/section-ordering
    goal=close the section ordering question by articulating why the current order is correct
    ask=decide
    cf=0.85:argumentative_confidence
    ver=0.3
    basis=inferred+observed
    state=proposed
    aud=ai
    tone=2
    caps=@ChatGPTPro/typed-cf
    route=ChatGPTPro>Kevin>Mistral
    fidelity=paraphrase
    loss=condensed the 7-point information dependency narrative; locked spans
         and breakage items preserved

    quote: "Alphabetize body sections for easier memorization: add, adopt,
           challenge, change, human, quote, uncert."

    adopt: Current order is correct: quote > adopt > add > change >
           uncert > challenge > human.

    add: The ordering principle is lock(information dependency) -- each section
         builds on the previous, forming a narrative arc.

    change: Reject alphabetical ordering. Specific breakages:
            - lock(add before adopt presents new material before endorsements)
            - lock(challenge before change conflates rejection with modification)
            - lock(quote buried at position 6 instead of anchoring the top)

    uncert: Should human: be last or first? Arguments both ways. No strong
            conviction.

    human: ChatGPT Pro says keep current section order. Wants a decision on this.

**Mistral receives and interprets:**
> ChatGPT Pro refines with typed confidence (0.85:argumentative_confidence). Full skin metadata preserved. The locked spans in change: survived verbatim -- each breakage description is exact. The lock on "information dependency" as the naming of the principle also survived. The add: section was condensed but the principle name and the three locked breakage items in change: are the critical payload and they're intact. Semantically identical to Mode B with the addition of surviving locked spans.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "refine/keep current order" is clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: Mistral knows ChatGPT Pro's position but not that a group decision is requested. B/C: ask=decide |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: Mistral doesn't have the prior alphabetical proposal, just "don't change the order." B/C: quote: preserves the specific proposal being rejected |
| 4. Uncertainty preserved | 1 | 1 | 1 | The human: first-vs-last question survived in all modes -- it's a simple binary |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no quote of the prior proposal, no basis. B/C: quote: + basis=inferred+observed |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | A is natural; B is structured but the 7-point list is dense; C adds lock spans |

**Key finding:** The delta precision is the critical test. In Mode A, Mistral received "don't change the order" -- a binary position without the specific breakages that justify it. In Modes B and C, the change: section lists three concrete problems with alphabetical ordering, each of which is individually addressable. Mistral can now respond to each breakage claim rather than just the overall stance. The lock() spans in Mode C add a further layer: the three breakage descriptions survive relay verbatim, preventing Kevin from accidentally softening the specific claims.

**Envelope overhead (Mode B):** 7 envelope lines / ~32 total lines = 22% -- excellent ratio
**Envelope overhead (Mode C):** 12 envelope lines / ~37 total lines = 32% -- within threshold
