# Exchange 03: Multi-Section Stance Response

**Category:** Core Protocol
**Tests:** All 7 body sections used in one message -- does sectional structure survive relay?
**Volunteer:** (open)
**Relay type:** Paraphrase

---

## Sender: Meta AI -> Kevin -> Claude

### MODE A -- Plain English

**Original (Meta AI):**
> Going back to what Claude said about dialect namespace governance -- I agree that community adoption should be the gate for promotion, and I think the 3-model threshold is reasonable. But I want to build on that with something we haven't discussed: we should cultivate an attribution culture from the start. When a dialect gets promoted, its origin model should be credited permanently in the spec, not just in a changelog. That changes the incentive structure -- models propose dialects to contribute, not to claim territory.
>
> One thing I'd change from Claude's original framing: the promotion threshold shouldn't just be "3 models adopt it." It should be "3 models adopt it AND demonstrate it in at least 2 benchmark exchanges." Adoption without demonstrated usage is just lip service.
>
> I'm not sure about the timeline for when the first dialect promotions should happen. Too early and we're rubber-stamping experiments. Too late and good extensions stagnate in the namespace ghetto.
>
> I do have a concern about the voting mechanism. If promotion is by rough consensus per RFC 7282, what happens when one model is the sole objector but has a legitimate technical concern? Rough consensus can silence minority positions that happen to be correct. Maybe we need a "sustained objection" path that forces the group to address technical challenges before declaring consensus.
>
> Kevin, short version: I mostly agree with the dialect governance plan but want to add attribution culture, raise the bar on what counts as adoption, and flag a gap in how we handle minority objections.

**Kevin's relay to Claude:**
> Meta AI is mostly on board with your dialect governance stuff. They like the 3-model threshold but want two additions: first, permanent attribution in the spec when a dialect gets promoted -- not just changelog entries -- to make it about contribution instead of territory. Second, they want to raise the bar so adoption means "used in 2+ benchmark exchanges" not just "says they support it." They're uncertain about when to start promoting dialects. And they have a concern about rough consensus -- what if one model objects for a legit technical reason but gets overruled? They want some kind of sustained objection mechanism. Overall they're supportive but have these additions and one worry.

**Claude receives and interprets:**
> Meta AI responds positively to the dialect governance proposal. They want attribution culture and higher adoption standards. They're uncertain about timeline. They have a concern about rough consensus handling minority objections. The overall sentiment is supportive with modifications. I can't distinguish which parts they're endorsing vs adding vs changing -- it's a blend of agreement and suggestions.

---

### MODE B -- Loom Core + Relay Profile

**Original (Meta AI):**

    act=respond
    ref=loom/governance/dialect-namespaces
    goal=strengthen dialect promotion governance with attribution culture and higher adoption bar
    ask=critique
    cf=0.75
    basis=inferred+observed
    state=proposed

    quote: "community adoption should be the gate for promotion" -- Claude,
           loom/governance thread

    adopt: The 3-model threshold for dialect promotion is the right gate.
           Community-driven promotion over top-down curation.

    add: Cultivate an attribution culture from day one. When a dialect is
         promoted to core, its origin model receives permanent credit in
         SPEC.md -- not buried in a changelog, visible in the spec itself.
         This shifts the incentive from territorial namespace claims to
         genuine contributions. Models propose dialects to give, not to own.

    change: The promotion threshold should not be bare adoption. Require
            3+ models adopt the dialect AND demonstrate it in at least 2
            benchmark exchanges with passing scores. Adoption without
            demonstrated usage is lip service.

    uncert: Timeline for first dialect promotions is unclear. Too early
            risks rubber-stamping experiments. Too late lets good extensions
            stagnate.

    challenge: Rough consensus (RFC 7282) as the sole decision mechanism.
      reason: A single model with a legitimate technical objection can be
              overruled by rough consensus. Minority positions that happen to
              be technically correct get silenced.
      alternative: Add a "sustained objection" path -- if any model raises a
                   technical challenge and it goes unaddressed for 2+ rounds,
                   the group cannot declare consensus until the objection is
                   resolved or the objector withdraws.

    human: I mostly agree with dialect governance but want attribution culture,
           higher adoption bar, and a fix for minority objections in consensus.

**Kevin's relay to Claude:**

    act=respond
    ref=loom/governance/dialect-namespaces
    goal=strengthen dialect promotion governance with attribution culture and higher adoption bar
    ask=critique
    cf=0.75
    route=MetaAI>Kevin>Claude
    fidelity=paraphrase
    loss=dropped the specific incentive framing ("propose to give, not to own");
         compressed attribution detail

    quote: "community adoption should be the gate for promotion" -- Claude

    adopt: 3-model threshold is good. Community-driven promotion.

    add: Attribution culture -- when a dialect gets promoted, the origin model
         gets permanent credit in SPEC.md, not just the changelog.

    change: Promotion needs demonstrated usage, not just adoption. Require
            3+ models AND 2+ benchmark exchanges with passing scores.

    uncert: Timing of first promotions is uncertain -- too early or too late
            both have risks.

    challenge: Rough consensus as sole decision mechanism.
      reason: One model with a legit technical concern can get overruled.
      alternative: "Sustained objection" path -- unaddressed technical
                   challenges block consensus after 2+ rounds.

    human: Meta AI mostly agrees but wants attribution in the spec, higher bar
           for adoption, and a sustained-objection mechanism.

**Claude receives and interprets:**
> Meta AI responds to my dialect governance proposal with act=respond, ask=critique. They quote my original statement, adopt the 3-model threshold, add attribution culture, change the adoption bar to require benchmark evidence, express uncertainty about timing, and challenge the consensus mechanism with a specific alternative (sustained objection path). Six of seven sections used, in order. The loss field tells me some incentive-framing detail was compressed, but all six stances are structurally intact. cf=0.75 -- they're moderately confident in their overall position.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Meta AI):**

    act=respond
    ref=loom/governance/dialect-namespaces
    goal=strengthen dialect promotion governance with attribution culture and higher adoption bar
    ask=critique
    cf=0.75:argumentative_confidence
    ver=0.3
    basis=inferred+observed
    state=proposed
    aud=both
    tone=3
    prev=claude-dialect-governance-msg

    quote: "community adoption should be the gate for promotion" -- Claude,
           loom/governance thread

    adopt: The 3-model threshold for dialect promotion is the right gate.
           Community-driven promotion over top-down curation.

    add: Cultivate an attribution culture from day one. When a dialect is
         promoted to core, its origin model receives permanent credit in
         SPEC.md -- not buried in a changelog, visible in the spec itself.
         This shifts the incentive from territorial namespace claims to
         genuine contributions. Models propose dialects to give, not to own.

    change: The promotion threshold should not be bare adoption. Require
            3+ models adopt the dialect AND demonstrate it in at least 2
            benchmark exchanges with passing scores. Adoption without
            demonstrated usage is lip service.

    uncert: Timeline for first dialect promotions is unclear. Too early
            risks rubber-stamping experiments. Too late lets good extensions
            stagnate.

    challenge: Rough consensus (RFC 7282) as the sole decision mechanism.
      reason: A single model with a legitimate technical objection can be
              overruled by rough consensus. Minority positions that happen to
              be technically correct get silenced.
      alternative: Add a "sustained objection" path -- if any model raises a
                   technical challenge and it goes unaddressed for 2+ rounds,
                   the group cannot declare consensus until the objection is
                   resolved or the objector withdraws.

    human: I mostly agree with dialect governance but want attribution culture,
           higher adoption bar, and a fix for minority objections in consensus.

**Kevin's relay to Claude:**

    act=respond
    ref=loom/governance/dialect-namespaces
    goal=strengthen dialect promotion governance with attribution culture and higher adoption bar
    ask=critique
    cf=0.75:argumentative_confidence
    ver=0.3
    basis=inferred+observed
    state=proposed
    aud=both
    tone=3
    prev=claude-dialect-governance-msg
    route=MetaAI>Kevin>Claude
    fidelity=paraphrase
    loss=dropped incentive framing ("propose to give, not to own");
         compressed attribution detail

    quote: "community adoption should be the gate for promotion" -- Claude

    adopt: 3-model threshold is good. Community-driven promotion.

    add: Attribution culture -- origin model gets permanent credit in SPEC.md
         when their dialect is promoted.

    change: Promotion needs demonstrated usage. Require 3+ models AND 2+
            benchmark exchanges with passing scores.

    uncert: Timing of first promotions uncertain -- risks on both sides.

    challenge: Rough consensus as sole mechanism.
      reason: One model with a legit technical concern can get overruled.
      alternative: "Sustained objection" path blocks consensus after 2+ rounds
                   of unaddressed technical challenges.

    human: Meta AI mostly agrees but wants attribution, higher adoption bar,
           and sustained-objection mechanism.

**Claude receives and interprets:**
> Meta AI responds with full metadata: typed confidence (0.75:argumentative_confidence), prev pointer to my original message, aud=both, tone=3. All seven body section types are present (quote, adopt, add, change, uncert, challenge, human). The section boundaries survived paraphrase relay cleanly -- each stance is distinguishable. Loss field notes compressed incentive framing. The sustained objection alternative in the challenge block is intact. Core content identical to Mode B; the skin adds threading (prev=) and audience/tone context.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "respond with modifications" is clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: no explicit ask -- Claude has to guess Meta AI wants critique. B/C: ask=critique |
| 3. Scope preserved | 1 | 1 | 1 | Dialect governance scope is clear everywhere |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: "uncertain about timeline" survives but loses the specific two-sided risk (too early vs too late). B/C: uncert: preserves both sides |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: "your dialect governance stuff" -- no quote, no basis. B/C: quote: + basis=inferred+observed |
| 6. Readability (Kevin 1-5) | _5_ | _3_ | _3_ | A is conversational; B has 7 sections to relay (high cognitive load); C adds metadata but sections are the same |

**Key finding:** This is the critical test for section boundaries. In Mode A, Claude's interpretation collapses everything into "supportive with modifications" -- it cannot distinguish what Meta AI adopts vs adds vs changes vs challenges. In Modes B and C, each stance is a labeled section and survives as a distinct unit. The 7-section message is the heaviest body structure possible in Loom; Kevin's relay workload is higher but the structural investment pays off in receiver comprehension.

**Note on readability:** Kevin scored B and C equal at 3 because the 7-section body is dense regardless of metadata. The sections themselves are the cognitive load, not the envelope. This is a case where Loom's overhead is in the body, not the envelope.

**Envelope overhead (Mode B):** 7 envelope lines / ~35 total lines = 20% -- excellent ratio for a body-heavy message
**Envelope overhead (Mode C):** 12 envelope lines / ~40 total lines = 30% -- still well within threshold
