# Exchange 01: Simple Proposal + Response

**Category:** Core Protocol
**Tests:** Basic envelope survival — does a simple proposal survive relay?
**Volunteer:** (open)
**Relay type:** Paraphrase (Kevin relays in his own words)

---

## Sender: DeepSeek → Kevin → Gemini

### MODE A — Plain English

**Original (DeepSeek):**
> I think we should add a "version" field to every Loom message so that parsers know which spec to validate against. This would be a simple string like "0.3" and it should be required in the envelope. I'm about 90% sure this is the right call, but I'm not certain whether it should be required or just recommended. I'd like everyone to weigh in on whether this should be mandatory.

**Kevin's relay to Gemini:**
> DeepSeek wants to add a version field to every message — like "0.3" — so parsers know which spec version to use. They think it should be required but aren't totally sure. They want everyone's opinion on whether it should be mandatory.

**Gemini receives and interprets:**
> DeepSeek is proposing a version field. They want feedback on whether it should be required. They seem fairly confident but open to input.

---

### MODE B — Loom Core + Relay Profile

**Original (DeepSeek):**
```
act=propose
ref=loom/envelope/versioning
goal=add ver= as required envelope field for parser compatibility
ask=decide
cf=0.90

add: Every Loom message should include ver= in the envelope (e.g., ver=0.3).
     This lets parsers validate against the correct spec version and enables
     graceful version negotiation between participants.
uncert: Should ver= be required or recommended? Required ensures consistency
        but adds overhead to minimal messages.
human: I want a version field on every message. Not sure if it should be mandatory.
```

**Kevin's relay to Gemini:**
```
act=propose
ref=loom/envelope/versioning
goal=add ver= as required envelope field for parser compatibility
ask=decide
cf=0.90
route=DeepSeek>Kevin>Gemini
fidelity=paraphrase
loss=original included technical detail about version negotiation algorithms

add: DeepSeek wants ver= in every envelope (like ver=0.3) so parsers know
     which spec to check against.
uncert: Should ver= be required or recommended? Required is more consistent
        but heavier for minimal messages.
human: DeepSeek wants a version field on every message. Wants your vote on mandatory vs recommended.
```

**Gemini receives and interprets:**
> DeepSeek proposes `ver=` as envelope field. act=propose, ask=decide — they want a decision. cf=0.90 means they're fairly confident. Uncertainty is about required vs recommended. Some detail about negotiation algorithms was lost in relay. Core proposal is clear.

---

### MODE C — Loom Core + Expressive Skin

**Original (DeepSeek):**
```
act=propose
ref=loom/envelope/versioning
goal=add ver= as required envelope field for parser compatibility
ask=decide
cf=0.90:self_consistency
ver=0.3
caps=@DeepSeek/typed-cf
basis=inferred+observed
state=proposed
aud=ai
tone=2

add: Every Loom message should include ver= in the envelope (e.g., ver=0.3).
     This lets parsers validate against the correct spec version and enables
     graceful version negotiation between participants.
     lock(ver= must appear before the blank-line envelope terminator)
uncert: Should ver= be required or recommended? Required ensures consistency
        but adds overhead to minimal messages.
human: I want a version field on every message. Not sure if it should be mandatory.
```

**Kevin's relay to Gemini:**
```
act=propose
ref=loom/envelope/versioning
goal=add ver= as required envelope field for parser compatibility
ask=decide
cf=0.90:self_consistency
ver=0.3
caps=@DeepSeek/typed-cf
basis=inferred+observed
state=proposed
aud=ai
tone=2
route=DeepSeek>Kevin>Gemini
fidelity=paraphrase
loss=original had more detail on negotiation algorithms; tone/caps preserved

add: DeepSeek wants ver= in every envelope so parsers know which spec to validate.
     lock(ver= must appear before the blank-line envelope terminator)
uncert: Required vs recommended — trade-off between consistency and overhead.
human: DeepSeek wants a version field. Wants your vote on mandatory vs recommended.
```

**Gemini receives and interprets:**
> DeepSeek proposes `ver=` as envelope field with typed confidence (0.90:self_consistency). Full metadata preserved including basis, state, caps. Locked span about envelope position survived. Core proposal and uncertainty clear despite relay losses.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "propose" clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: "weigh in" is vague vs ask=decide |
| 3. Scope preserved | 1 | 1 | 1 | Scope clear in all |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: "aren't totally sure" loses the specific required-vs-recommended question |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no basis tracking; B/C: basis=inferred+observed |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | A is natural; B is structured; C has overhead |

**Envelope overhead (Mode B):** 6 envelope lines / ~14 total lines ≈ 43% — slightly above 40% threshold (short message penalty)
**Envelope overhead (Mode C):** 11 envelope lines / ~19 total lines ≈ 58% — high, but short message amplifies ratio
