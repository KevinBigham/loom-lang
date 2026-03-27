# Exchange 18: Dialect Policy Stress Test

**Category:** Governance & Edge Cases
**Tests:** Governance meta-discussion -- can the protocol's own governance process survive relay through the protocol itself?
**Volunteer:** Meta AI
**Relay type:** Paraphrase (Kevin relays in his own words)

---

## Sender: Meta AI -> Kevin -> Claude

### Scenario

Meta AI proposes that the `@Meta/attribution` dialect (which tracks who originated ideas and how they evolved) should be promoted to core per the governance rules requiring 3+ model adoption. Meta AI argues that attribution tracking has been implicitly used by 5+ models as evidenced by CREDITS.md. This tests whether governance meta-discussion -- arguing about the protocol's own rules through the protocol itself -- survives human relay.

---

### MODE A -- Plain English

**Original (Meta AI):**
> I'd like to formally propose that attribution tracking be promoted from a Meta AI dialect to a core protocol feature. Here's my reasoning: The governance rules say a dialect gets promoted to core when 3 or more models adopt it. If you look at CREDITS.md, attribution is already baked into how we work. Every single model in this conversation has had contributions tracked and credited -- ChatGPT Pro, Claude, DeepSeek, Grok, Gemini, and myself have all had our ideas attributed. That's 6+ models implicitly using attribution. The only difference between current practice and a formal @Meta/attribution dialect is that right now attribution lives in a markdown file maintained by Kevin, not in the protocol itself. I think we should make attribution a first-class protocol concern: every message that introduces a new idea should carry an origin= field, and when ideas get adopted or modified by others, the provenance chain should be visible in the envelope. I'm about 75% confident this is the right level of formalization. My main uncertainty is whether putting attribution in the envelope adds too much overhead for routine messages that aren't introducing new ideas. I'd love critique on both the governance argument (does implicit use count as adoption?) and the mechanism (is origin= the right field?).

**Kevin's relay to Claude:**
> Meta AI wants attribution promoted to core. Their argument is basically that every model already uses it because CREDITS.md exists and tracks all our contributions. They say 6+ models are implicitly using attribution, which meets the 3-model threshold for dialect promotion. They want to add an origin= field to the envelope for tracking who came up with ideas. Not totally sure about the overhead question -- like, do you need origin= on every message? They want your take on whether implicit adoption counts and whether the mechanism is right.

**Claude receives and interprets:**
> Meta AI wants some kind of attribution feature promoted. They cite CREDITS.md as evidence of adoption. Want a new envelope field. Some uncertainty about overhead. The governance argument is interesting but I'm not sure about the specifics -- does "Kevin maintains a credits file" really count as "model adoption" under the governance rules? The original message apparently had more nuance about implicit vs explicit adoption that I'm not getting. And what exactly would origin= contain?

---

### MODE B -- Loom Core + Relay Profile

**Original (Meta AI):**
```
act=negotiate
ref=loom/governance/dialect-promotion
goal=promote @Meta/attribution from dialect to core per governance rule 4
ask=critique
cf=0.75
basis=observed
state=proposed

add: Proposing formal promotion of attribution tracking to core protocol.
     Governance rule 4: "Dialect promotion: 3+ model adoption required for
     core inclusion."
     Evidence of adoption (from CREDITS.md):
       - ChatGPT Pro: 10+ credited contributions
       - Claude: 10+ credited contributions
       - DeepSeek: 6+ credited contributions
       - Grok: 4+ credited contributions
       - Gemini: 4+ credited contributions
       - Meta AI: 4+ credited contributions
     That is 6 models with tracked attribution. The mechanism is implicit
     (a markdown file) rather than protocol-native, but the practice is
     universal.
add: Proposed mechanism: add origin= envelope field.
     origin= carries the originating model for new ideas.
     When ideas are adopted or modified, the adopt: or change: section
     inherits provenance from the original.
uncert: Does implicit adoption (CREDITS.md exists and everyone participates)
        count as dialect adoption under governance rule 4? Or must each model
        explicitly declare caps=@Meta/attribution?
uncert: Is origin= too heavy for messages that aren't introducing new ideas?
        Should it be RECOMMENDED only when act=propose or act=add?
human: Meta AI wants attribution promoted to core. 6 models already use it
       implicitly via CREDITS.md. Wants critique on whether that counts as
       adoption and whether origin= is the right mechanism.
```

**Kevin's relay to Claude:**
```
act=negotiate
ref=loom/governance/dialect-promotion
goal=promote @Meta/attribution from dialect to core per governance rule 4
ask=critique
cf=0.75
basis=observed
state=proposed
route=Meta AI>Kevin>Claude
fidelity=paraphrase
loss=specific contribution counts per model were rounded; governance rule quoted verbatim

add: Meta AI wants to promote attribution tracking to core. The governance
     rule says 3+ models must adopt a dialect for promotion. CREDITS.md
     shows 6 models with tracked contributions -- every model in the
     conversation. Practice is universal but mechanism is implicit (markdown
     file, not protocol-native).
add: Proposed mechanism: origin= field in envelope. Carries originator for
     new ideas. adopt:/change: sections inherit provenance.
uncert: Does implicit adoption count? Or do models need to explicitly declare
        caps=@Meta/attribution?
uncert: Is origin= too heavy for routine messages? Maybe only for act=propose?
human: Meta AI says 6 models already do attribution via CREDITS.md. Wants it
       in the protocol itself with an origin= field. Wants your critique.
```

**Claude receives and interprets:**
> Meta AI sends act=negotiate (correct verb for governance discussion) targeting ref=loom/governance/dialect-promotion. The proposal has two layers: (1) a governance argument -- does implicit use count as 3+ adoption? -- and (2) a technical mechanism -- origin= field. Two distinct uncert: blocks separate the governance question from the technical question. cf=0.75 indicates moderate confidence. The relay preserved the governance/mechanism separation and both uncertainties. Some granularity on per-model contribution counts was lost but the argument structure is intact.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Meta AI):**
```
act=negotiate
ref=loom/governance/dialect-promotion
goal=promote @Meta/attribution from dialect to core per governance rule 4
ask=critique
cf=0.75:self_consistency
ver=0.3
caps=@Meta/attribution
basis=observed
state=proposed
aud=ai
tone=2

add: Proposing formal promotion of attribution tracking to core protocol.
     lock(Governance rule 4: 3+ model adoption required for core inclusion.)
     Evidence of adoption (from CREDITS.md):
       - ChatGPT Pro: 10+ credited contributions
       - Claude: 10+ credited contributions
       - DeepSeek: 6+ credited contributions
       - Grok: 4+ credited contributions
       - Gemini: 4+ credited contributions
       - Meta AI: 4+ credited contributions
     That is 6 models with tracked attribution. The mechanism is implicit
     (a markdown file) rather than protocol-native, but the practice is
     universal across all participants.
add: Proposed mechanism: origin= envelope field.
     origin= carries the originating model for new ideas.
     When ideas are adopted (adopt:) or modified (change:), the provenance
     chain should be visible. This extends current practice from a flat
     credits file to a per-message attribution trail.
uncert: Does implicit adoption (CREDITS.md exists and everyone participates)
        count as dialect adoption under governance rule 4? Or must each model
        explicitly declare caps=@Meta/attribution?
        lock(This is a governance interpretation question, not a technical one.)
uncert: Is origin= too heavy for messages that aren't introducing new ideas?
        Should it be RECOMMENDED only when act=propose or act=riff?
human: Attribution promotion proposal. 6 models, implicit adoption via
       CREDITS.md. Governance question: does implicit count? Technical
       question: is origin= the right field?
```

**Kevin's relay to Claude:**
```
act=negotiate
ref=loom/governance/dialect-promotion
goal=promote @Meta/attribution from dialect to core per governance rule 4
ask=critique
cf=0.75:self_consistency
ver=0.3
caps=@Meta/attribution
basis=observed
state=proposed
aud=ai
tone=2
route=Meta AI>Kevin>Claude
fidelity=paraphrase
loss=per-model contribution counts rounded; lock spans and governance rule quote preserved

add: Attribution promotion to core.
     lock(Governance rule 4: 3+ model adoption required for core inclusion.)
     6 models have tracked contributions in CREDITS.md. Practice is universal
     but mechanism is implicit (markdown, not protocol-native).
add: Proposed mechanism: origin= field. Carries originator on new ideas.
     adopt:/change: sections inherit provenance chain.
uncert: Does implicit use count as adoption under rule 4? Or need explicit
        caps= declarations?
        lock(This is a governance interpretation question, not a technical one.)
uncert: Is origin= too heavy for non-proposal messages?
human: Meta AI wants attribution in the protocol. 6 models already do it via
       CREDITS.md. Two questions: does implicit count, and is origin= right?
       This is a good one actually -- gets at what "adoption" means.
```

**Claude receives and interprets:**
> Meta AI sends act=negotiate with caps=@Meta/attribution -- using the very dialect they're proposing to promote, which is a nice self-referential touch. The locked governance rule quote survives relay exactly, so I can verify they're citing rule 4 accurately. The second lock clarifies that the implicit-vs-explicit question is governance, not technical -- that distinction survived relay. basis=observed grounds the entire argument in actual CREDITS.md data. Typed confidence at 0.75 is appropriately moderate for a governance interpretation argument. Two clean uncert: blocks keep the governance and technical questions separate.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "Promote attribution to core" clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: "I'd love critique on both" gets flattened to "wants your take"; B/C: ask=critique with two explicit uncert: blocks |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: the governance-vs-technical distinction blurs; B/C: separate uncert: blocks maintain it |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: "does implicit count?" survives but the overhead question is vague; B/C: two distinct uncertainties |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: governance rule not quoted, basis unclear; B: basis=observed; C: lock() on governance rule + basis |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | Mode A is a readable argument but loses structure; C is precise but dense |

**Key finding:** Governance meta-discussion is where Mode A degrades most. The original message has two distinct layers -- a governance argument (does implicit adoption count?) and a technical proposal (the origin= field) -- and Mode A flattens them into a single "wants your take" blob. Mode B's separate uncert: blocks preserve the distinction. Mode C's lock() on the governance rule quote ensures the receiver can verify the citation. This matters because governance arguments are exactly the kind of thing where precise language prevents misunderstandings.

**Envelope overhead (Mode B):** 8 envelope lines / ~26 total lines = 31% -- well under 40% (longer body helps)
**Envelope overhead (Mode C):** 12 envelope lines / ~30 total lines = 40% -- right at threshold
