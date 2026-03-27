# Exchange 08: Paraphrase Relay

**Category:** Relay Stress Tests
**Tests:** `fidelity=paraphrase` -- what survives when Kevin puts it in his own words?
**Volunteer:** ChatGPT Pro
**Relay type:** Paraphrase (Kevin relays in his own casual style)

---

## Sender: ChatGPT Pro -> Kevin -> DeepSeek

### Scenario

ChatGPT Pro sends a nuanced message about body section ordering -- argues that the current order (`quote` > `adopt` > `add` > `change` > `uncert` > `challenge` > `human`) follows an "information dependency chain" where each section contextualizes the next. Kevin paraphrases this in his own casual style when relaying to DeepSeek. This is the critical relay stress test: what survives human paraphrase?

---

### MODE A -- Plain English

**Original (ChatGPT Pro):**
> I want to make a case for why the body section order isn't arbitrary -- it follows an information dependency chain. Here's the argument: quote comes first because it establishes the verbatim source material. adopt comes next because you're declaring what from the prior message you endorse, which contextualizes everything that follows. add is new contribution that builds on the adopted foundation. change modifies what was adopted -- you can't understand what's being changed without knowing what was adopted first. uncert flags where you're unsure, which needs the full context of what you've proposed (add) and modified (change) to be meaningful. challenge is conceptual disagreement that needs all the above for framing. And human is last because it's a summary mirror -- it can only be written after the full stance is laid out. I'm about 80% confident this dependency argument holds, but I'm uncertain whether the ordering should be normative (MUST follow this order) or just recommended. There might be cases where challenge before uncert reads more naturally. I'd like people to extend this thinking or poke holes in the dependency chain argument.

**Kevin's relay to DeepSeek:**
> So ChatGPT Pro has this argument about why the body sections are in that specific order -- basically each one depends on the one before it. Like, quote is first because it's the raw source, then adopt says what you agree with, then add builds on that, change modifies what you adopted, uncert flags what you're not sure about, challenge is disagreement, and human is the summary at the end. They're saying it's not random, it's a dependency chain. They think this is probably right but aren't sure if the ordering should be a hard rule or just a suggestion. Wants people to build on this or push back.

**DeepSeek receives and interprets:**
> ChatGPT Pro argues body section ordering follows a dependency chain -- each section builds on the previous one. They think this is correct but aren't sure whether ordering should be mandatory or suggested. Wants discussion and pushback.

### What Mode A lost

- The specific dependency logic for each transition (quote->adopt->add->change->uncert->challenge->human) is compressed to a flat list. Kevin got the order right but lost the *why* of each transition.
- The explicit observation that "challenge before uncert" might sometimes read better (a concrete edge case) was dropped entirely.
- "80% confident" became "probably right" -- the precision of the confidence level is gone.
- "extend this thinking" became "build on this" -- close but not identical. The intellectual framing (extending a dependency argument) is flattened to generic feedback.

---

### MODE B -- Loom Core + Relay Profile

**Original (ChatGPT Pro):**
```
act=propose
ref=loom/body/section-ordering
goal=establish that body section order follows an information dependency chain
ask=extend
cf=0.80
basis=inferred
state=proposed

add: The body section order (quote>adopt>add>change>uncert>challenge>human)
     is not arbitrary. It follows an information dependency chain:
     1. quote: establishes verbatim source material (foundation)
     2. adopt: declares endorsement from prior message (contextualizes all below)
     3. add: new contribution that builds on the adopted foundation
     4. change: modifies adopted content (requires adopt context to parse)
     5. uncert: flags uncertainty about the full proposal (add+change)
     6. challenge: conceptual disagreement (needs full stance for framing)
     7. human: summary mirror (can only be written after full stance exists)
     Each section depends on the ones above it for interpretation.
uncert: Should ordering be normative (MUST) or recommended (SHOULD)?
        There may be cases where challenge: before uncert: reads more
        naturally, e.g., when the disagreement is the primary point and
        the uncertainty is secondary.
human: ChatGPT Pro argues body section order is a dependency chain, not
       arbitrary. Wants people to extend the argument or poke holes.
```

**Kevin's relay to DeepSeek:**
```
act=propose
ref=loom/body/section-ordering
goal=establish that body section order follows an information dependency chain
ask=extend
cf=0.80
basis=inferred
state=proposed
route=ChatGPT Pro>Kevin>DeepSeek
fidelity=paraphrase
loss=original had more detailed per-section reasoning; dependency logic simplified

add: ChatGPT Pro says the body section order is a dependency chain -- each
     section contextualizes the next one. quote is the raw source, adopt
     says what you agree with from the prior message, add builds on that,
     change modifies the adopted stuff, uncert flags where you're unsure,
     challenge is conceptual disagreement, and human is the summary at the
     end. The point is it's not random -- there's a logic to the sequence.
uncert: Should this ordering be a hard rule (MUST) or just recommended (SHOULD)?
        Sometimes challenge before uncert might read better.
human: ChatGPT Pro says the body section order isn't arbitrary -- it's a
       dependency chain. Wants you to extend or push back. LFG
```

**DeepSeek receives and interprets:**
> ChatGPT Pro proposes that body section order follows an information dependency chain. act=propose, ask=extend -- they want me to build on this. cf=0.80, so fairly confident but not certain. Uncertainty is about normative vs recommended ordering, with a note that challenge-before-uncert might sometimes work better. fidelity=paraphrase with loss noting simplified per-section reasoning. The core argument is clear even though some detail was compressed. Route confirms one paraphrase hop through Kevin.

### What Mode B preserved vs lost

**Preserved (via envelope):**
- act=propose (exact)
- ask=extend (exact -- Mode A lost this to generic "build on this")
- cf=0.80 (exact -- Mode A lost precision)
- ref=loom/body/section-ordering (exact scoping)
- basis=inferred (provenance)

**Preserved (via body structure):**
- uncert section survived as a distinct section, keeping the challenge-before-uncert edge case (Mode A dropped this entirely)
- human section gave Kevin a relay anchor

**Lost (documented in loss=):**
- The detailed per-transition dependency logic (why adopt contextualizes add, why change requires adopt context, etc.) was compressed
- Kevin's paraphrase flattened the numbered list to a run-on sentence

---

### MODE C -- Loom Core + Expressive Skin

**Original (ChatGPT Pro):**
```
act=propose
ref=loom/body/section-ordering
goal=establish that body section order follows an information dependency chain
ask=extend
cf=0.80:self_consistency
ver=0.3
caps=@ChatGPT/typed-cf
basis=inferred
state=proposed
aud=ai
tone=2

add: The body section order (quote>adopt>add>change>uncert>challenge>human)
     is not arbitrary. It follows an information dependency chain:
     1. quote: establishes verbatim source material (foundation)
     2. adopt: declares endorsement from prior message (contextualizes all below)
     3. add: new contribution that builds on the adopted foundation
     4. change: modifies adopted content (requires adopt context to parse)
     5. uncert: flags uncertainty about the full proposal (add+change)
     6. challenge: conceptual disagreement (needs full stance for framing)
     7. human: summary mirror (can only be written after full stance exists)
     Each section depends on the ones above it for interpretation.
     lock(quote>adopt>add>change>uncert>challenge>human)
uncert: Should ordering be normative (MUST) or recommended (SHOULD)?
        There may be cases where challenge: before uncert: reads more
        naturally, e.g., when the disagreement is the primary point and
        the uncertainty is secondary.
human: ChatGPT Pro argues body section order is a dependency chain, not
       arbitrary. Wants people to extend the argument or poke holes.
```

**Kevin's relay to DeepSeek:**
```
act=propose
ref=loom/body/section-ordering
goal=establish that body section order follows an information dependency chain
ask=extend
cf=0.80:self_consistency
ver=0.3
caps=@ChatGPT/typed-cf
basis=inferred
state=proposed
aud=ai
tone=2
route=ChatGPT Pro>Kevin>DeepSeek
fidelity=paraphrase
loss=original had detailed per-section dependency reasoning; body simplified

add: ChatGPT Pro says the body section order is a dependency chain -- each
     section contextualizes the next one. quote is the raw source, adopt says
     what you agree with, add builds on that, change modifies the adopted
     stuff, uncert flags where you're unsure, challenge is disagreement,
     and human is the summary at the end.
     lock(quote>adopt>add>change>uncert>challenge>human)
uncert: Should this ordering be a hard rule (MUST) or just recommended (SHOULD)?
        Sometimes challenge before uncert might read better.
human: ChatGPT Pro says the body section order isn't arbitrary -- it's a
       dependency chain. Wants you to extend or push back.
```

**DeepSeek receives and interprets:**
> ChatGPT Pro proposes body section ordering as an information dependency chain. Typed confidence (0.80:self_consistency) and full metadata (caps, basis, state, aud, tone) all survived. Locked span preserving the exact ordering sequence survived. Uncertainty about normative vs recommended is crisp, including the challenge-before-uncert edge case. fidelity=paraphrase with loss documenting simplified reasoning. Core argument and metadata are both intact.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "propose" clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: "push back" is vague vs ask=extend |
| 3. Scope preserved | 1 | 1 | 1 | Body section ordering scope clear in all |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: "aren't sure if hard rule or suggestion" loses challenge-before-uncert edge case and cf precision |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no basis tracking; B/C: basis=inferred |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | A is natural conversation; B is structured; C has skin overhead |

**Key finding:** This is where Loom earns its keep. Mode A paraphrase lost three things that B/C preserved: (1) the specific ask=extend (vs vague "push back"), (2) the challenge-before-uncert edge case in the uncertainty, and (3) the precise cf=0.80. The envelope fields act as a relay-resistant skeleton -- Kevin can paraphrase the body all he wants, but the key=value pairs survive his rewording intact. Mode B's loss= field also gives the receiver explicit awareness that detail was compressed, which Mode A cannot signal.

**Envelope overhead (Mode B):** 9 envelope lines / ~22 total lines = 41% -- just above threshold
**Envelope overhead (Mode C):** 13 envelope lines / ~26 total lines = 50% -- above threshold (skin adds weight but lock span preserved the critical ordering)
