# Exchange 02: Structured Disagreement

**Category:** Core Protocol
**Tests:** `challenge:` with `reason:` + alternative -- does structured disagreement survive relay?
**Volunteer:** Claude
**Relay type:** Paraphrase

---

## Sender: Claude -> Kevin -> Grok

### MODE A -- Plain English

**Original (Claude):**
> I don't think we should make the ABNF grammar normative in v0.3. We have exactly zero real multi-model exchanges to base it on, which means any grammar we write now will be codifying guesses. There's direct precedent for this going badly: FIPA-ACL wrote their agent communication grammar up front, and it was largely ignored because it locked in assumptions that didn't match how agents actually communicated once deployed. My recommendation is to iterate from examples through v0.5, maintain a non-normative ABNF appendix as scaffolding that people can reference without being bound by, and only promote it to normative status at v1.0 once the benchmark has shown us what the real grammar looks like. I'm roughly 80% confident this is the right path, though I acknowledge the inflection point could come earlier -- maybe v0.5 -- if benchmark patterns crystallize faster than I expect.

**Kevin's relay to Grok:**
> So Claude doesn't want to make the grammar official yet. Basically says we have no real data to base it on and points to some old protocol called FIPA-ACL that crashed and burned because they formalized their grammar too early. Claude thinks we should keep working from examples and have the grammar just be a reference appendix until v1.0, or maybe v0.5 if things come together sooner. Pretty confident about this one.

**Grok receives and interprets:**
> Claude opposes making the grammar normative now. Something about a historical protocol that formalized too early and failed. Wants to wait until v1.0 or possibly v0.5. Fairly confident. No specific alternative structure was communicated -- just "wait and use examples."

---

### MODE B -- Loom Core + Relay Profile

**Original (Claude):**

    act=challenge
    ref=loom/grammar/normative-status
    goal=defer normative ABNF to v1.0; keep non-normative appendix as scaffolding
    ask=decide
    cf=0.80
    basis=observed+inferred
    state=proposed

    adopt: The protocol needs a formal grammar eventually. No disagreement there.

    challenge: Making ABNF normative in v0.3.
      reason: We have 0 real multi-model exchanges to base the grammar on.
              FIPA-ACL wrote its grammar first and it was largely ignored --
              the grammar codified assumptions that did not survive contact
              with real agent-to-agent usage. Premature formalization freezes
              bad patterns.
      alternative: Iterate from worked examples for v0.2 through v0.5. Maintain
                   a non-normative ABNF appendix as scaffolding. Promote to
                   normative at v1.0 after benchmark data reveals what the actual
                   grammar IS -- not what we guessed it would be.

    uncert: The right moment to formalize might be v0.5 rather than v1.0 if
            the benchmark reveals clear patterns early. I don't have strong
            conviction on the exact version cutoff.

    human: I think formalizing the grammar now is premature. Let's wait for benchmark data.

**Kevin's relay to Grok:**

    act=challenge
    ref=loom/grammar/normative-status
    goal=defer normative ABNF to v1.0; keep non-normative appendix as scaffolding
    ask=decide
    cf=0.80
    route=Claude>Kevin>Grok
    fidelity=paraphrase
    loss=condensed FIPA-ACL historical detail; dropped specific version range (v0.2-v0.5)

    adopt: We need a grammar eventually -- Claude agrees on that.

    challenge: Making the grammar official in v0.3.
      reason: No real exchanges exist yet to base a grammar on. Claude says
              FIPA-ACL tried this and it flopped because the grammar locked
              in wrong assumptions.
      alternative: Keep using examples for now. Have a draft grammar appendix
                   that's not binding. Make it official at v1.0 when we have
                   real data from the benchmark.

    uncert: Maybe v0.5 instead of v1.0 if patterns emerge early.

    human: Claude says don't formalize the grammar yet -- wait for benchmark results.

**Grok receives and interprets:**
> Claude challenges making ABNF normative at v0.3. act=challenge, ask=decide -- they want a group decision. The challenge has explicit structure: reason is lack of real data plus FIPA-ACL precedent, alternative is iterate-then-formalize at v1.0. Some historical detail was lost per the loss field, but the core argument structure survived. cf=0.80 with uncertainty about whether v0.5 might be the right cutoff instead of v1.0.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Claude):**

    act=challenge
    ref=loom/grammar/normative-status
    goal=defer normative ABNF to v1.0; keep non-normative appendix as scaffolding
    ask=decide
    cf=0.80:self_consistency
    ver=0.3
    basis=observed+inferred
    state=proposed
    aud=ai
    tone=2
    caps=@Claude/typed-cf

    adopt: The protocol needs a formal grammar eventually. No disagreement there.

    challenge: Making ABNF normative in v0.3.
      reason: We have 0 real multi-model exchanges to base the grammar on.
              FIPA-ACL wrote its grammar first and it was largely ignored --
              the grammar codified assumptions that did not survive contact
              with real agent-to-agent usage. Premature formalization freezes
              bad patterns. lock(Premature formalization freezes bad patterns.)
      alternative: Iterate from worked examples for v0.2 through v0.5. Maintain
                   a non-normative ABNF appendix as scaffolding. Promote to
                   normative at v1.0 after benchmark data reveals what the actual
                   grammar IS -- not what we guessed it would be.

    uncert: The right moment to formalize might be v0.5 rather than v1.0 if
            the benchmark reveals clear patterns early. I don't have strong
            conviction on the exact version cutoff.

    human: I think formalizing the grammar now is premature. Let's wait for benchmark data.

**Kevin's relay to Grok:**

    act=challenge
    ref=loom/grammar/normative-status
    goal=defer normative ABNF to v1.0; keep non-normative appendix as scaffolding
    ask=decide
    cf=0.80:self_consistency
    ver=0.3
    basis=observed+inferred
    state=proposed
    aud=ai
    tone=2
    caps=@Claude/typed-cf
    route=Claude>Kevin>Grok
    fidelity=paraphrase
    loss=condensed FIPA-ACL historical detail; dropped specific version range (v0.2-v0.5)

    adopt: We need a grammar eventually -- Claude agrees on that.

    challenge: Making the grammar official in v0.3.
      reason: No real exchanges exist yet. FIPA-ACL tried this and it flopped.
              lock(Premature formalization freezes bad patterns.)
      alternative: Keep iterating from examples. Draft grammar appendix stays
                   non-binding. Promote to normative at v1.0 after benchmark data.

    uncert: Maybe v0.5 instead of v1.0 if patterns emerge early.

    human: Claude says don't formalize the grammar yet -- wait for benchmark results.

**Grok receives and interprets:**
> Claude challenges making ABNF normative at v0.3 with typed confidence (0.80:self_consistency). Full metadata preserved: basis, state, caps, tone. The locked span about premature formalization survived verbatim. Challenge structure (reason + alternative) is intact. Some FIPA-ACL detail compressed per loss field but the argument's skeleton is fully legible. Core semantics identical to Mode B.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "challenge" is clear in all modes -- Claude disagrees |
| 2. Requested action | 0 | 1 | 1 | Mode A: Kevin said "pretty confident" -- no ask for a decision. Grok has no idea a group decision is expected. B/C: ask=decide explicit |
| 3. Scope preserved | 1 | 1 | 1 | The scope (ABNF normative status in v0.3) is clear across all modes |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: "maybe v0.5 if things come together sooner" survives vaguely but the specific uncertainty (version cutoff conditional on benchmark patterns) is softened to nothing. B/C: uncert: item preserved |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: "some old protocol called FIPA something?" -- Kevin half-remembers the name, no basis tracking. B/C: basis=observed+inferred, FIPA-ACL named in reason: |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | A is natural conversation; B requires reading structure; C has metadata overhead |

**Key finding:** The structured alternative is the critical loss in Mode A. Grok interpreted Claude's position as "wait and use examples" -- a vague deferral. In Modes B and C, the alternative is explicit and actionable: non-normative appendix as scaffolding, promote at v1.0 after benchmark data. The reason/alternative pairing survived relay as a unit because Kevin could see the sublabels and knew to preserve both halves.

**Envelope overhead (Mode B):** 7 envelope lines / ~24 total lines = 29% -- well within the 40% threshold
**Envelope overhead (Mode C):** 12 envelope lines / ~29 total lines = 41% -- at the threshold; skin fields add ~12 percentage points
