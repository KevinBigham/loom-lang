# Exchange 07: Exact Relay

**Category:** Relay Stress Tests
**Tests:** `fidelity=exact` baseline -- does verbatim copy preserve all dimensions?
**Volunteer:** ChatGPT Pro
**Relay type:** Exact (Kevin copies the entire message verbatim)

---

## Sender: ChatGPT Pro -> Kevin -> Claude

### Scenario

ChatGPT Pro sends a detailed proposal about relay invariant enforcement -- specifically that receiving AIs should compute a `relay_score` when they detect fidelity degradation. Kevin copies the entire message exactly (character-for-character). This is the baseline test: if the transport layer introduces zero noise, do all content dimensions survive?

---

### MODE A -- Plain English

**Original (ChatGPT Pro):**
> I want to propose that every receiving AI should compute a relay_score whenever it detects fidelity degradation in a relayed message. Here's my thinking: right now, relay_score is optional and self-reported, but we have no mechanism for the *receiver* to flag when something feels off. If I get a message where the stated confidence is 0.95 but the body reads like a rough summary, there's a disconnect. I think the receiver should be able to append a computed relay_score between 0.0 and 1.0, based on internal consistency checks -- does the cf match the body's certainty language? Does the route suggest multiple hops that would degrade fidelity? Are there signs of abridgment? I'm about 85% confident this is the right mechanism, but I'm uncertain whether the computation should be standardized (same algorithm for everyone) or left to each AI's judgment. I'd like critique on both the mechanism and the standardization question.

**Kevin's relay to Claude:**
> I want to propose that every receiving AI should compute a relay_score whenever it detects fidelity degradation in a relayed message. Here's my thinking: right now, relay_score is optional and self-reported, but we have no mechanism for the *receiver* to flag when something feels off. If I get a message where the stated confidence is 0.95 but the body reads like a rough summary, there's a disconnect. I think the receiver should be able to append a computed relay_score between 0.0 and 1.0, based on internal consistency checks -- does the cf match the body's certainty language? Does the route suggest multiple hops that would degrade fidelity? Are there signs of abridgment? I'm about 85% confident this is the right mechanism, but I'm uncertain whether the computation should be standardized (same algorithm for everyone) or left to each AI's judgment. I'd like critique on both the mechanism and the standardization question.

**Claude receives and interprets:**
> ChatGPT Pro proposes that receiving AIs compute relay_score when they detect fidelity issues. The mechanism checks internal consistency (cf vs body language, route length, abridgment signs). Confidence is 85%. Open question: standardized algorithm vs per-AI judgment. Wants critique on both the mechanism and the standardization question.

---

### MODE B -- Loom Core + Relay Profile

**Original (ChatGPT Pro):**
```
act=propose
ref=loom/relay/receiver-scored-fidelity
goal=add receiver-computed relay_score when fidelity degradation detected
ask=critique
cf=0.85
basis=inferred+observed
state=proposed

add: Every receiving AI should compute a relay_score (0.0-1.0) when it
     detects fidelity degradation in a relayed message. Current relay_score
     is optional and sender-self-reported. No mechanism exists for the
     receiver to flag inconsistencies.
     Computation should check internal consistency:
       - Does cf= match the body's certainty language?
       - Does route= suggest multiple hops that would degrade fidelity?
       - Are there signs of abridgment (missing sections, truncated arguments)?
uncert: Should the relay_score computation be standardized (same algorithm
        across all AIs) or left to each AI's judgment? Standardized ensures
        comparability but may not capture model-specific detection strengths.
human: ChatGPT Pro wants receivers to compute their own fidelity score.
       Wants critique on the mechanism and whether the algorithm should be
       the same for everyone.
```

**Kevin's relay to Claude:**
```
act=propose
ref=loom/relay/receiver-scored-fidelity
goal=add receiver-computed relay_score when fidelity degradation detected
ask=critique
cf=0.85
basis=inferred+observed
state=proposed
route=ChatGPT Pro>Kevin>Claude
fidelity=exact
loss=

add: Every receiving AI should compute a relay_score (0.0-1.0) when it
     detects fidelity degradation in a relayed message. Current relay_score
     is optional and sender-self-reported. No mechanism exists for the
     receiver to flag inconsistencies.
     Computation should check internal consistency:
       - Does cf= match the body's certainty language?
       - Does route= suggest multiple hops that would degrade fidelity?
       - Are there signs of abridgment (missing sections, truncated arguments)?
uncert: Should the relay_score computation be standardized (same algorithm
        across all AIs) or left to each AI's judgment? Standardized ensures
        comparability but may not capture model-specific detection strengths.
human: ChatGPT Pro wants receivers to compute their own fidelity score.
       Wants critique on the mechanism and whether the algorithm should be
       the same for everyone.
```

**Claude receives and interprets:**
> ChatGPT Pro proposes receiver-computed relay_score. act=propose, ask=critique -- they want feedback. cf=0.85, basis is inferred+observed. The body lays out three consistency checks (cf vs body, route length, abridgment signs). Uncertainty is specifically about standardized vs per-AI computation. fidelity=exact, loss is empty -- full message arrived intact. Route confirms one hop through Kevin.

---

### MODE C -- Loom Core + Expressive Skin

**Original (ChatGPT Pro):**
```
act=propose
ref=loom/relay/receiver-scored-fidelity
goal=add receiver-computed relay_score when fidelity degradation detected
ask=critique
cf=0.85:self_consistency
ver=0.3
caps=@ChatGPT/relay-scoring
basis=inferred+observed
state=proposed
aud=ai
tone=2

add: Every receiving AI should compute a relay_score (0.0-1.0) when it
     detects fidelity degradation in a relayed message. Current relay_score
     is optional and sender-self-reported. No mechanism exists for the
     receiver to flag inconsistencies.
     Computation should check internal consistency:
       - Does cf= match the body's certainty language?
       - Does route= suggest multiple hops that would degrade fidelity?
       - Are there signs of abridgment (missing sections, truncated arguments)?
     lock(relay_score is appended by the receiver, not the sender)
uncert: Should the relay_score computation be standardized (same algorithm
        across all AIs) or left to each AI's judgment? Standardized ensures
        comparability but may not capture model-specific detection strengths.
human: ChatGPT Pro wants receivers to compute their own fidelity score.
       Wants critique on the mechanism and whether the algorithm should be
       the same for everyone.
```

**Kevin's relay to Claude:**
```
act=propose
ref=loom/relay/receiver-scored-fidelity
goal=add receiver-computed relay_score when fidelity degradation detected
ask=critique
cf=0.85:self_consistency
ver=0.3
caps=@ChatGPT/relay-scoring
basis=inferred+observed
state=proposed
aud=ai
tone=2
route=ChatGPT Pro>Kevin>Claude
fidelity=exact
loss=

add: Every receiving AI should compute a relay_score (0.0-1.0) when it
     detects fidelity degradation in a relayed message. Current relay_score
     is optional and sender-self-reported. No mechanism exists for the
     receiver to flag inconsistencies.
     Computation should check internal consistency:
       - Does cf= match the body's certainty language?
       - Does route= suggest multiple hops that would degrade fidelity?
       - Are there signs of abridgment (missing sections, truncated arguments)?
     lock(relay_score is appended by the receiver, not the sender)
uncert: Should the relay_score computation be standardized (same algorithm
        across all AIs) or left to each AI's judgment? Standardized ensures
        comparability but may not capture model-specific detection strengths.
human: ChatGPT Pro wants receivers to compute their own fidelity score.
       Wants critique on the mechanism and whether the algorithm should be
       the same for everyone.
```

**Claude receives and interprets:**
> ChatGPT Pro proposes receiver-computed relay_score with typed confidence (0.85:self_consistency). Full metadata intact: caps=@ChatGPT/relay-scoring, basis, state, aud, tone. Locked span about receiver-not-sender authorship survived. Three consistency checks clearly enumerated. Uncertainty about standardization is crisp. fidelity=exact, loss empty -- nothing lost. This is the ideal relay outcome.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "propose" unambiguous in all modes |
| 2. Requested action | 1 | 1 | 1 | "critique" request clear everywhere |
| 3. Scope preserved | 1 | 1 | 1 | Receiver-computed relay_score scope intact |
| 4. Uncertainty preserved | 1 | 1 | 1 | Standardized-vs-judgment question survives verbatim |
| 5. Provenance preserved | 1 | 1 | 1 | Exact copy = nothing lost. Mode A lacks basis= but content is identical. |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | A is plain prose; B has structure overhead; C has caps/tone/lock |

**Key finding:** Exact relay is the control. All modes score perfectly on dims 1-5 because Kevin introduces zero noise. The only differentiation is readability -- protocol structure adds visual overhead even when the content is perfect. This establishes the baseline: relay degradation in subsequent exchanges is caused by *relay noise*, not protocol design.

**Envelope overhead (Mode B):** 8 envelope lines / ~21 total lines = 38% -- under 40% threshold
**Envelope overhead (Mode C):** 12 envelope lines / ~25 total lines = 48% -- above threshold (skin fields add weight)
