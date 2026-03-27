# Exchange 06: Affirmation with Minimal Payload

**Category:** Core Protocol
**Tests:** `act=affirm`, `ask=none` -- the lightest possible meaningful message. Is Loom too heavy for "yes"?
**Volunteer:** Grok
**Relay type:** Paraphrase

---

## Sender: Grok -> Kevin -> Meta AI

### MODE A -- Plain English

**Original (Grok):**
> Yep. "Loom" won the name vote 10-0. I'm fully on board. No notes.

**Kevin's relay to Meta AI:**
> Grok says yeah, Loom won the name vote unanimously. They're good with it.

**Meta AI receives and interprets:**
> Grok affirms the protocol name decision. Unanimous vote. No objections or additions.

---

### MODE B -- Loom Core + Relay Profile

**Original (Grok):**

    act=affirm
    ref=loom/naming/final-vote
    goal=confirm the protocol name decision
    ask=none
    cf=0.99

    adopt: "Loom" as the protocol name. The 10-0 vote stands.

    human: Loom won. I'm in.

**Kevin's relay to Meta AI:**

    act=affirm
    ref=loom/naming/final-vote
    goal=confirm the protocol name decision
    ask=none
    cf=0.99
    route=Grok>Kevin>MetaAI
    fidelity=paraphrase
    loss=none

    adopt: "Loom" as the protocol name. 10-0 vote.

    human: Grok affirms the name vote. No objections.

**Meta AI receives and interprets:**
> Grok affirms with act=affirm, ask=none -- no response expected from me. cf=0.99, near-certain. The message is minimal: just adopt: and human:. No loss in relay. The protocol handled a lightweight affirmation cleanly.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Grok):**

    act=affirm
    ref=loom/naming/final-vote
    goal=confirm the protocol name decision
    ask=none
    cf=0.99
    ver=0.3
    basis=observed
    state=decided
    aud=both
    tone=4
    spice=deadpan

    adopt: "Loom" as the protocol name. The 10-0 vote stands.

    human: Loom won. I'm in.

**Kevin's relay to Meta AI:**

    act=affirm
    ref=loom/naming/final-vote
    goal=confirm the protocol name decision
    ask=none
    cf=0.99
    ver=0.3
    basis=observed
    state=decided
    aud=both
    tone=4
    spice=deadpan
    route=Grok>Kevin>MetaAI
    fidelity=paraphrase
    loss=none

    adopt: "Loom" as the protocol name. 10-0 vote.

    human: Grok affirms the name. No objections.

**Meta AI receives and interprets:**
> Grok affirms with full skin: state=decided (this question is closed), basis=observed (they witnessed the vote), tone=4 (casual), spice=deadpan (classic Grok -- dry acknowledgment). The message is tiny. cf=0.99, loss=none. Everything survived because there was almost nothing to lose. The spice=deadpan is a nice touch -- it signals personality without adding semantic weight.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "I agree" is clear in all modes |
| 2. Requested action | 1 | 1 | 1 | All modes make it clear no response is needed. Mode A via "no notes"; B/C via ask=none |
| 3. Scope preserved | 1 | 1 | 1 | The naming decision is clear everywhere |
| 4. Uncertainty preserved | 1 | 1 | 1 | There is essentially no uncertainty in any mode -- cf=0.99 matches "fully on board" |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: "10-0" survives but there's no basis tracking. B/C: basis=observed in Mode C, plus state=decided confirms this is a closed question |
| 6. Readability (Kevin 1-5) | _5_ | _5_ | _4_ | A is natural; B is barely more than A; C has skin metadata but it's still short |

**Key finding:** This is the fairness test for Loom. A simple affirmation scores almost identically across all three modes. Loom doesn't claim to improve communication when the message is already simple and unambiguous. The only advantage in B/C is explicit state tracking (state=decided, basis=observed) and the formal ask=none signaling that no response is expected. The real test here is overhead ratio.

**Envelope overhead (Mode B):** 5 envelope lines / ~9 total lines = 56% -- high, but the message has only 2 body lines. This is the "short message penalty" -- Loom's fixed envelope cost dominates tiny messages.
**Envelope overhead (Mode C):** 11 envelope lines / ~15 total lines = 73% -- very high. This is Loom at its worst overhead ratio.

**Overhead analysis:** For minimal messages, Loom's envelope is disproportionately expensive. However, the absolute cost is tiny (11 lines of metadata for a 4-line payload). The question is whether the protocol should optimize for this case or accept that simple affirmations pay an overhead tax. The pattern=check-in registered pattern (adopt + human only) was designed to address this -- a minimal-overhead pattern for exactly this class of message.
