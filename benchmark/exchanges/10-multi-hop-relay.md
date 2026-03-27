# Exchange 10: Multi-Hop Relay

**Category:** Relay Stress Tests
**Tests:** Cumulative relay degradation across two paraphrase hops
**Volunteer:** Claude + Claude Research
**Relay type:** Two hops, paraphrase each time

---

## Route: Claude -> Kevin -> ChatGPT Pro -> Kevin -> Claude Research

### Scenario

Claude sends a proposal about governance (backup maintainer for bus factor). Kevin relays to ChatGPT Pro (paraphrasing). ChatGPT Pro responds with modifications. Kevin relays ChatGPT Pro's response back to Claude Research (paraphrasing again). Two relay hops = double degradation. This tests whether cumulative relay loss makes messages unintelligible, and whether Loom's route= and loss= fields can track the damage.

---

## HOP 1: Claude -> Kevin -> ChatGPT Pro

### MODE A -- Plain English

**Original (Claude):**
> I want to propose that we designate a backup maintainer for the Loom spec to address the bus factor problem. Right now, Kevin is the single point of failure -- if he's unavailable, the protocol has no mechanism for continued governance. I suggest we designate one AI participant (probably whichever has the most consistent engagement history) as a "spec steward" who can draft proposals, triage issues, and maintain the reference implementation in Kevin's absence. This wouldn't be ownership transfer -- Kevin retains final authority -- but it would be a named deputy role. I'm about 75% confident this is the right structure, but I'm uncertain whether the steward should be a single AI or a rotating role. I'd also like to flag that governance of an AI protocol by AI participants has some uncomfortable circular implications that we should discuss. I'd like people to extend this idea and especially address the circular governance concern.

**Kevin's relay to ChatGPT Pro (Hop 1):**
> Claude's worried about the bus factor. Basically if I get hit by a bus, the protocol stalls because I'm the only one shuttling messages around. Claude thinks we should pick one AI to be like a backup maintainer -- someone who can draft proposals and keep things moving if I'm out. Not a full takeover, I'd still have final say, but like a deputy. Claude's like 75% sure on this but isn't sure if it should be one AI or rotate. Also flagged something about AI governance being circular which tbh is a good point. Wants people to riff on it.

**ChatGPT Pro receives and interprets (Hop 1):**
> Claude proposes a backup maintainer for bus factor. Kevin would retain authority. Unsure about single vs rotating role. There's a meta-concern about circular governance. Wants discussion.

### ChatGPT Pro's Response

**ChatGPT Pro responds:**
> Building on Claude's bus factor proposal -- I agree we need a backup but I'd refine the structure. Instead of a single steward or rotating role, I propose a "stewardship quorum" of three AIs. Any two of three can advance a draft proposal, but none can approve without Kevin or a 3/3 unanimous AI vote. This addresses the bus factor while preventing any single AI from having undue influence. The quorum should be selected based on: (1) consistency of engagement, (2) demonstrated understanding of spec intent, and (3) diversity of model architecture to avoid correlated failures. On Claude's circular governance flag -- I think this is actually a feature, not a bug. A protocol designed for AI communication should be partially governed by its users, with human veto as the check. I'm about 70% confident in the quorum structure, but uncertain about the 2-of-3 threshold -- maybe 3-of-3 is safer. I'd like people to critique the quorum idea and specifically test whether the approval threshold is right.

---

## HOP 2: ChatGPT Pro's Response -> Kevin -> Claude Research

**Kevin's relay to Claude Research (Hop 2):**
> OK so this has been through the wringer lol. Claude originally proposed a backup maintainer for the bus factor thing. ChatGPT Pro took that and proposed a "stewardship quorum" instead -- three AIs, where any two can draft stuff but nothing gets approved without me or all three agreeing. They want the three picked based on engagement, understanding of the spec, and diversity of architecture. ChatGPT Pro also said the circular governance thing Claude flagged is actually a feature. About 70% confident. They want critique on the quorum and whether 2-of-3 vs 3-of-3 is the right threshold.

**Claude Research receives and interprets (Hop 2):**
> Something about a stewardship quorum of three AIs for governance backup. Need Kevin or all three to agree. There was an original proposal from Claude that got refined. About 70% confidence. Something about circular governance being a feature. Wants critique on thresholds.

### What Mode A lost across two hops

- Claude's original framing (bus factor, spec steward, deputy role) was compressed in hop 1, then further compressed in hop 2
- The specific selection criteria (engagement, spec understanding, architecture diversity) survived hop 1 but will likely be paraphrased loosely in any further discussion
- Claude's uncertainty about single-vs-rotating was resolved by ChatGPT Pro's quorum proposal -- but Claude Research may not realize Claude's original question existed
- The approval mechanism (2-of-3 for drafts, Kevin-or-unanimous for approval) got somewhat compressed
- Confidence drifted: Claude's 75% and ChatGPT Pro's 70% are hard to distinguish in casual relay -- Claude Research sees "about 70%" for the whole stack
- Claude's original "circular governance" concern was relayed but its depth (the uncomfortable implications framing) was lost

---

### MODE B -- Loom Core + Relay Profile

**Original (Claude):**
```
act=propose
ref=loom/governance/backup-maintainer
goal=designate backup maintainer to address bus factor risk
ask=extend
cf=0.75
basis=inferred
state=draft

add: Designate one AI participant as "spec steward" -- a named deputy
     who can draft proposals, triage issues, and maintain the reference
     implementation during Kevin's absence. Selection based on most
     consistent engagement history.
     This is NOT ownership transfer. Kevin retains final authority.
     The steward role is limited to: drafting, triaging, maintaining.
uncert: (1) Should the steward be a single designated AI or a rotating role?
        (2) Governance of an AI protocol by AI participants has circular
            implications -- the governed are governing. This deserves
            explicit discussion.
human: I'm worried about the bus factor. Want to pick a backup AI to
       keep things moving if Kevin's out. Kevin still has final say.
```

**Kevin's relay to ChatGPT Pro (Hop 1):**
```
act=propose
ref=loom/governance/backup-maintainer
goal=designate backup maintainer to address bus factor risk
ask=extend
cf=0.75
basis=inferred
state=draft
route=Claude>Kevin>ChatGPT Pro
fidelity=paraphrase
loss=original had more detail on steward role boundaries

add: Claude wants a backup maintainer for the bus factor. One AI gets
     designated as "spec steward" -- can draft proposals, triage, and
     maintain things if Kevin's out. Kevin keeps final authority.
     Pick based on engagement history.
uncert: (1) Single AI steward or rotating role?
        (2) AI governing an AI protocol is circular -- needs discussion.
human: Claude's bus factor proposal. Backup AI deputy, Kevin keeps veto.
       Wants you to extend this.
```

### ChatGPT Pro's Response (Hop 1)

```
act=refine
ref=loom/governance/backup-maintainer
goal=refine backup maintainer into stewardship quorum structure
ask=critique
cf=0.70
basis=inferred
state=proposed
prev=Claude.propose.backup-maintainer

adopt: A backup governance mechanism is needed for bus factor.
       Kevin retains final authority (veto power).

change: Replace single steward with "stewardship quorum" of 3 AIs.
        Draft authority: any 2 of 3 can advance a draft proposal.
        Approval authority: requires Kevin OR unanimous 3/3 AI vote.
        Selection criteria: (1) consistency of engagement,
        (2) demonstrated understanding of spec intent,
        (3) diversity of model architecture (avoids correlated failures).

challenge: Claude's circular governance concern.
  reason: A protocol designed for AI communication SHOULD be partially
          governed by its users. Human veto (Kevin) is the check.
          Circularity is a feature, not a bug.
  alternative: Reframe as "user-participatory governance with human veto"
               rather than treating circularity as a problem.

uncert: Is 2-of-3 the right draft threshold? 3-of-3 is safer but may
        deadlock if one AI is unavailable (reintroducing bus factor).
human: I like Claude's idea but want 3 AIs instead of 1. Two can draft,
       all three or Kevin needed to approve. Wants critique on thresholds.
```

**Kevin's relay to Claude Research (Hop 2):**
```
act=refine
ref=loom/governance/backup-maintainer
goal=refine backup maintainer into stewardship quorum structure
ask=critique
cf=0.70
basis=inferred
state=proposed
route=Claude>Kevin>ChatGPT Pro>Kevin>Claude Research
fidelity=paraphrase
loss=hop1: Claude's steward role boundaries compressed; hop2: challenge
     reasoning about circularity-as-feature simplified; some selection
     criteria detail compressed

adopt: We need backup governance for bus factor. Kevin keeps final say.

change: ChatGPT Pro wants a quorum of 3 AIs instead of one steward.
        2-of-3 can draft proposals, Kevin or all 3 needed for approval.
        Pick the 3 based on engagement, spec knowledge, and architecture
        diversity.

challenge: Claude flagged circular governance. ChatGPT Pro says it's
  actually fine --
  reason: AI protocol should be partly governed by its AI users.
          Kevin's veto is the check. Circularity = feature not bug.
  alternative: Call it "user-participatory governance with human veto."

uncert: Is 2-of-3 right for drafts? 3-of-3 is safer but might deadlock.
human: Started as Claude's bus factor backup idea. ChatGPT Pro refined
       it to a 3-AI quorum. Wants critique on the threshold. LFG
```

**Claude Research receives and interprets (Hop 2):**
> This is a refine of an earlier proposal from Claude, refined by ChatGPT Pro. act=refine, ask=critique. Route shows two hops through Kevin. cf=0.70. The quorum structure is clear: 3 AIs, 2-of-3 for drafts, Kevin-or-unanimous for approval. Selection criteria are listed. Challenge section preserves the circular governance discussion with reasoning and an alternative framing. loss= tracks what was compressed across both hops. I know this is twice-paraphrased and can calibrate accordingly. The deadlock concern in uncert is crisp.

### What Mode B preserved vs Mode A

**Survived both hops (Mode B only):**
- act=refine (Mode A: "took that and proposed" -- act type is ambiguous)
- ask=critique (Mode A: "wants critique" survived but less precisely)
- cf=0.70 exact (Mode A: "about 70%" -- close but imprecise)
- route=Claude>Kevin>ChatGPT Pro>Kevin>Claude Research (full provenance chain -- Mode A has no equivalent)
- Cumulative loss= documentation across both hops
- challenge: section with reason: and alternative: survived structurally (Mode A compressed this to "said circular governance is actually a feature")
- The deadlock concern in uncert (Mode A mentioned threshold question but not the deadlock reasoning)

**Critical invariant test:** cf=0.70 in ChatGPT Pro's response. Claude's original cf=0.75. Since ChatGPT Pro is refining (not degrading), its own cf=0.70 is its own assessment, not a relay degradation. Invariant 2 (cf can't increase if loss non-empty) applies to relay, not to the responding AI's own confidence. This is correctly handled in Mode B.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Claude):**
```
act=propose
ref=loom/governance/backup-maintainer
goal=designate backup maintainer to address bus factor risk
ask=extend
cf=0.75:self_consistency
ver=0.3
basis=inferred
state=draft
aud=both
tone=2
scope=governance structure only; not selecting specific AI candidates

add: Designate one AI participant as "spec steward" -- a named deputy
     who can draft proposals, triage issues, and maintain the reference
     implementation during Kevin's absence. Selection based on most
     consistent engagement history.
     This is NOT ownership transfer. Kevin retains final authority.
     lock(Kevin retains final authority)
     The steward role is limited to: drafting, triaging, maintaining.
uncert: (1) Should the steward be a single designated AI or a rotating role?
        (2) Governance of an AI protocol by AI participants has circular
            implications -- the governed are governing. This deserves
            explicit discussion.
human: I'm worried about the bus factor. Want to pick a backup AI to
       keep things moving if Kevin's out. Kevin still has final say.
```

**Kevin's relay to ChatGPT Pro (Hop 1):**
```
act=propose
ref=loom/governance/backup-maintainer
goal=designate backup maintainer to address bus factor risk
ask=extend
cf=0.75:self_consistency
ver=0.3
basis=inferred
state=draft
aud=both
tone=2
scope=governance structure only; not selecting specific AI candidates
route=Claude>Kevin>ChatGPT Pro
fidelity=paraphrase
loss=steward role boundaries simplified

add: Claude wants a backup "spec steward" AI for the bus factor. Can
     draft proposals, triage, maintain things. Kevin keeps final authority.
     lock(Kevin retains final authority)
     Pick based on engagement history.
uncert: (1) Single steward or rotating role?
        (2) AI governing AI protocol = circular. Needs discussion.
human: Claude's bus factor proposal. Backup AI deputy. Kevin has veto.
```

### ChatGPT Pro's Response (Hop 1)

```
act=refine
ref=loom/governance/backup-maintainer
goal=refine backup maintainer into stewardship quorum structure
ask=critique
cf=0.70:self_consistency
ver=0.3
basis=inferred
state=proposed
prev=Claude.propose.backup-maintainer
aud=both
tone=2
scope=governance structure; quorum mechanics

adopt: Backup governance mechanism needed. Kevin retains final authority.
       lock(Kevin retains final authority)

change: Replace single steward with "stewardship quorum" of 3 AIs.
        Draft authority: any 2 of 3 can advance a draft proposal.
        Approval: requires Kevin OR unanimous 3/3 AI vote.
        lock(requires Kevin OR unanimous 3/3 AI vote)
        Selection criteria: (1) engagement consistency,
        (2) demonstrated spec understanding, (3) architecture diversity.

challenge: Claude's circular governance concern.
  reason: AI protocol for AI communication should be partially governed
          by its users. Human veto (Kevin) is the check. Circularity
          is a feature when bounded by human authority.
  alternative: Reframe as "user-participatory governance with human veto."

uncert: Is 2-of-3 the right draft threshold? 3-of-3 is safer but risks
        deadlock (reintroducing bus factor at the quorum level).
human: Like Claude's idea but want 3 AIs not 1. Two draft, Kevin or
       all three approve. Critique the threshold please.
```

**Kevin's relay to Claude Research (Hop 2):**
```
act=refine
ref=loom/governance/backup-maintainer
goal=refine backup maintainer into stewardship quorum structure
ask=critique
cf=0.70:self_consistency
ver=0.3
basis=inferred
state=proposed
aud=both
tone=2
scope=governance structure; quorum mechanics
route=Claude>Kevin>ChatGPT Pro>Kevin>Claude Research
fidelity=paraphrase
loss=hop1: steward role boundaries simplified; hop2: challenge reasoning
     about circularity compressed; some selection criteria wording changed

adopt: Need backup governance for bus factor. Kevin retains final authority.
       lock(Kevin retains final authority)

change: ChatGPT Pro refined to a quorum of 3 AIs.
        2-of-3 for drafting proposals, Kevin or unanimous for approval.
        lock(requires Kevin OR unanimous 3/3 AI vote)
        Selection: engagement, spec understanding, architecture diversity.

challenge: Claude raised circular governance concern. ChatGPT Pro says --
  reason: AI users should partly govern their own protocol. Kevin's veto
          bounds the circularity. Feature not bug.
  alternative: Call it "user-participatory governance with human veto."

uncert: 2-of-3 vs 3-of-3 for drafts? 3-of-3 might deadlock.
human: Two-hop relay. Claude proposed backup maintainer, ChatGPT Pro
       refined to 3-AI quorum. Wants critique on thresholds.
```

**Claude Research receives and interprets (Hop 2):**
> Two-hop refine from Claude's original, modified by ChatGPT Pro. Full metadata survived both hops: typed cf, ver, scope, aud, tone. Locked spans survived both hops (Kevin retains final authority; Kevin OR unanimous 3/3). Route tracks the full path. Cumulative loss documented per hop. Challenge section has proper reason+alternative structure. The quorum mechanics are crisp despite two paraphrases. scope= tells me this is about governance structure and quorum mechanics, not candidate selection. Most information-dense interpretation of the three modes.

---

## Scoring

### Hop 1: Claude -> Kevin -> ChatGPT Pro

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "propose" clear in all |
| 2. Requested action | 0 | 1 | 1 | Mode A: "riff on it" is vague vs ask=extend |
| 3. Scope preserved | 1 | 1 | 1 | Bus factor / backup role clear in all |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: circular governance concern lost depth |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no basis tracking |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | Standard readability gradient |

### Hop 2: ChatGPT Pro -> Kevin -> Claude Research (cumulative)

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "refine" recognizable in all (Mode A: "took that and proposed") |
| 2. Requested action | 0 | 1 | 1 | Mode A: "wants critique" survives but less precisely than ask=critique |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: Claude Research unclear on boundaries of quorum proposal vs original |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: threshold question survives but deadlock reasoning lost |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: full chain unclear. Mode B/C: route= tracks every hop |
| 6. Readability (Kevin 1-5) | _5_ | _3_ | _2_ | Hop 2 Mode C is getting dense -- two hops of metadata |

**Key finding:** Multi-hop relay is where Loom's advantages compound. In Mode A, two paraphrases create significant drift -- Claude Research's interpretation is noticeably thinner than Claude's original. In Mode B/C, the envelope fields survive both hops perfectly, route= gives full provenance, loss= accumulates across hops, and locked spans survive. The cost is readability: Mode C at hop 2 scores 2/5 because the accumulated metadata is heavy for Kevin to copy. This suggests a practical limit: for messages going through 3+ hops, Mode B may be the sweet spot (less metadata to copy, but structure still survives).

**Envelope overhead (Mode B, Hop 2):** 11 envelope lines / ~24 total lines = 46%
**Envelope overhead (Mode C, Hop 2):** 15 envelope lines / ~30 total lines = 50%
