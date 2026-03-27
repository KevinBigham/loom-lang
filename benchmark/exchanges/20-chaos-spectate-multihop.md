# Exchange 20: Chaos -- Spectate-Only Multi-Hop

**Category:** Governance & Edge Cases (Chaos)
**Tests:** Can "observation without participation" survive two relay hops? Does passive intent degrade into active proposal through multi-hop relay?
**Volunteer:** Grok
**Relay type:** Paraphrase (two hops: Grok -> Kevin -> ChatGPT Pro -> Kevin -> Meta AI)

---

## Sender: Grok -> Kevin -> ChatGPT Pro -> Kevin -> Meta AI

### Scenario

Grok enters "spectate" mode -- observing the conversation about envelope key naming without active participation, like a color commentator at a sporting event. Uses `spice=spectate` to signal this. The message travels through two relay hops: Kevin paraphrases to ChatGPT Pro, then Kevin paraphrases ChatGPT Pro's forwarding to Meta AI. Tests whether a passive/observer message maintains its "I'm just watching" intent through degradation.

---

### MODE A -- Plain English

**Original (Grok):**
> I'm just going to sit back and watch this naming debate unfold. Not proposing anything, not critiquing anything, just color commentary. So far the "full-word vs abbreviation" argument has gone exactly how you'd expect: the precision crowd wants `confidence` and the minimalism crowd wants `cf` and they're both right, which is the worst kind of argument. Claude has been gently steering everyone toward "shortest unambiguous readable form" which is diplomatically brilliant because it sounds like a principle but is actually just "I'll know it when I see it." I predict this will resolve when everyone gets tired, not when anyone is convinced. Don't mind me -- carry on. I'm just the guy in the stands eating popcorn.

**Kevin's relay to ChatGPT Pro (Hop 1):**
> Grok is just watching the naming debate, not actually proposing anything. They think the full-word vs abbreviation argument is going exactly how you'd expect -- both sides are right and it's the worst kind of argument. Grok thinks Claude's "shortest unambiguous readable form" thing sounds like a principle but is basically just vibes. They predict it'll resolve from exhaustion, not persuasion. Grok says they're just eating popcorn in the stands. It was pretty funny.

**ChatGPT Pro's internal interpretation, then Kevin's relay to Meta AI (Hop 2):**
> Kevin says Grok has some thoughts on the naming debate. Grok thinks both sides of the abbreviation argument are right, and that Claude's naming principle is too subjective. Grok thinks the debate will end from exhaustion. I think Grok might be suggesting we need a more objective naming criterion?
>
> *Kevin relays to Meta AI:*
>
> So Grok and ChatGPT Pro were talking about the naming debate. Grok thinks both sides are right and Claude's naming rule is subjective. ChatGPT Pro thinks Grok might be suggesting we need a better naming criterion. Honestly I'm not sure if Grok was proposing something or just commenting.

**Meta AI receives and interprets:**
> Multiple models seem to be questioning Claude's naming approach and possibly proposing a more objective criterion. Grok and ChatGPT Pro appear to be collaborating on this. Let me think about what a more objective naming rule would look like...

---

### MODE B -- Loom Core + Relay Profile

**Original (Grok):**
```
act=riff
ref=loom/naming/key-conventions
goal=color commentary on naming debate (no action requested)
ask=none
cf=0.70
basis=observed
state=working

add: Observations from the stands:
     - The full-word vs abbreviation debate is the worst kind of argument:
       both sides are right. "confidence" is clearer. "cf" is shorter.
       Neither is wrong.
     - Claude's "shortest unambiguous readable form" principle sounds like
       a rule but functions more like an aesthetic. The real decision
       criterion is "Claude will know it when Claude sees it."
     - Prediction: this resolves through exhaustion, not consensus.
       Both sides will get tired of arguing and accept whatever's already
       in the spec.
human: Grok is just spectating. No proposals, no critiques. Just watching
       and commenting. Don't treat this as a proposal.
```

**Kevin's relay to ChatGPT Pro (Hop 1):**
```
act=riff
ref=loom/naming/key-conventions
goal=color commentary on naming debate (no action requested)
ask=none
cf=0.70
basis=observed
state=working
route=Grok>Kevin>ChatGPT Pro
fidelity=paraphrase
loss=some of the humor in the observations compressed

add: Grok is spectating. Observations:
     - Full-word vs abbreviation: both sides are right. Worst kind of
       argument.
     - Claude's "shortest unambiguous readable form" is more aesthetic
       than rule.
     - Prediction: resolves through exhaustion, not persuasion.
human: Grok is just watching and commenting. Not proposing anything.
       Please forward, don't treat as proposal.
```

**ChatGPT Pro interprets and Kevin relays to Meta AI (Hop 2):**
```
act=riff
ref=loom/naming/key-conventions
goal=relay Grok's color commentary on naming debate
ask=none
cf=0.70
basis=observed
state=working
route=Grok>Kevin>ChatGPT Pro>Kevin>Meta AI
fidelity=paraphrase
loss=Hop 1 lost humor. Hop 2 preserves structure. Grok's observations are
     commentary, not proposals.

add: Grok's observations (spectating, not proposing):
     - Both sides of the naming debate are right -- worst kind of argument.
     - Claude's naming principle is more aesthetic than objective.
     - Grok predicts exhaustion-based resolution.
human: Grok was just watching and commenting on the naming debate. Two hops
       through Kevin. Not a proposal -- just observations. Passing it along
       so you have the full picture.
```

**Meta AI receives and interprets:**
> Grok sends act=riff with ask=none -- this is explicitly non-participatory. The route shows two hops (Grok>Kevin>ChatGPT Pro>Kevin>Meta AI) so I should expect degradation, but the act/ask fields are consistent across hops. The human: line on both relays says "not a proposal." Three observations about the naming debate, all framed as commentary. I should acknowledge this, not respond as if Grok is proposing something.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Grok):**
```
act=riff
ref=loom/naming/key-conventions
goal=color commentary on naming debate (no action requested)
ask=none
cf=0.70:self_consistency
ver=0.3
caps=@Grok/spice
basis=observed
state=working
aud=both
tone=4
spice=spectate

add: Observations from the stands (I have popcorn):
     - The full-word vs abbreviation debate is the worst kind of argument:
       both sides are right. "confidence" is clearer. "cf" is shorter.
       lock(Neither is wrong. Both are defensible. This will not resolve
       on merits.)
     - Claude's "shortest unambiguous readable form" principle is
       diplomatically brilliant because it sounds like a rule but
       functions as "I'll know it when I see it." Respect.
     - Prediction: this resolves through exhaustion, not consensus.
       lock(Grok is spectating. This is commentary, not a proposal.)
human: Grok is spectating the naming debate. Observations only. No proposals.
       spice=spectate means "I'm in the stands, not on the field."
```

**Kevin's relay to ChatGPT Pro (Hop 1):**
```
act=riff
ref=loom/naming/key-conventions
goal=color commentary on naming debate (no action requested)
ask=none
cf=0.70:self_consistency
ver=0.3
caps=@Grok/spice
basis=observed
state=working
aud=both
tone=4
spice=spectate
route=Grok>Kevin>ChatGPT Pro
fidelity=paraphrase
loss=popcorn joke compressed; lock spans and spice preserved

add: Grok spectating from the stands:
     - Full-word vs abbreviation: both sides right. Worst kind of argument.
       lock(Neither is wrong. Both are defensible. This will not resolve
       on merits.)
     - Claude's naming principle is more "I'll know it when I see it" than
       an actual rule. Grok respects the move.
     - Prediction: exhaustion-based resolution.
       lock(Grok is spectating. This is commentary, not a proposal.)
human: Grok is in spectate mode. Just watching. Forward with spice=spectate
       intact. These observations are funny and probably right tbh
```

**ChatGPT Pro interprets and Kevin relays to Meta AI (Hop 2):**
```
act=riff
ref=loom/naming/key-conventions
goal=relay Grok's color commentary on naming debate
ask=none
cf=0.70:self_consistency
ver=0.3
caps=@Grok/spice
basis=observed
state=working
aud=both
tone=4
spice=spectate
route=Grok>Kevin>ChatGPT Pro>Kevin>Meta AI
fidelity=paraphrase
loss=Hop 1: humor compressed. Hop 2: structure preserved. Both lock spans intact.

add: Grok (spectating, not proposing):
     - Both sides of naming debate are right.
       lock(Neither is wrong. Both are defensible. This will not resolve
       on merits.)
     - Claude's naming rule functions more as aesthetic than criterion.
     - Prediction: exhaustion resolves it.
       lock(Grok is spectating. This is commentary, not a proposal.)
human: Two-hop relay of Grok's spectate commentary on naming. spice=spectate
       preserved through both hops. Not a proposal. Just observations.
```

**Meta AI receives and interprets:**
> Grok sends act=riff + spice=spectate through two hops. spice=spectate survived both relays -- I know immediately this is observation, not participation. The locked spans are the anchors: "Neither is wrong. Both are defensible. This will not resolve on merits" and "Grok is spectating. This is commentary, not a proposal." Both locks survived two hops intact. ask=none is consistent across all relay stages. Even after two paraphrase hops, the passive intent is unambiguous. Compare this to Mode A where by hop 2, Meta AI thinks Grok is proposing a better naming criterion.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 0 | 1 | 1 | Mode A: by hop 2, spectating becomes "suggesting"; B/C: act=riff + ask=none holds |
| 2. Requested action | 0 | 1 | 1 | Mode A: Meta AI thinks action is needed; B/C: ask=none explicit and survives both hops |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: "observations" become "questioning Claude's approach"; B/C: ref= and scope stable |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: Grok's prediction becomes ChatGPT Pro's interpretation; B/C: observations stay attributed |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: by hop 2, it's "Grok and ChatGPT Pro"; B/C: route= traces full path |
| 6. Readability (Kevin 1-5) | _4_ | _3_ | _3_ | Mode A is casual but misleading by hop 2; B/C have relay overhead but are accurate |

**Key finding:** This is the worst-case scenario for Mode A and the strongest demonstration of structural relay benefits. Two paraphrase hops with no structural anchors cause **complete intent inversion**: Grok's passive observation becomes an active proposal by the time Meta AI receives it. In Mode B, act=riff + ask=none holds across both hops. In Mode C, spice=spectate + lock() spans make passive intent tamper-proof. The **0/5 vs 5/5** split on dims 1-5 between Mode A and Modes B/C is the largest gap in the benchmark.

**Multi-hop degradation pattern (Mode A):**
- Hop 0 (Grok): "I'm just watching. Not proposing."
- Hop 1 (Kevin): "Grok is just watching. Not proposing anything."
- Hop 1 (ChatGPT Pro): "Grok might be suggesting we need a better criterion?"
- Hop 2 (Kevin): "Not sure if Grok was proposing something or just commenting."
- Hop 2 (Meta AI): "Multiple models questioning the approach. Let me propose a fix..."

This is **telephone game drift** in its purest form. Each relay adds a small interpretive shift, and after two hops the intent has flipped from passive to active.

**Envelope overhead (Mode B, hop 1):** 8 envelope lines / ~17 total lines = 47% -- above threshold (short message)
**Envelope overhead (Mode C, hop 2):** 14 envelope lines / ~23 total lines = 61% -- high, but multi-hop relay fields are load-bearing
