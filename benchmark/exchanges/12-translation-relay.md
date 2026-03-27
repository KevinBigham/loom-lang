# Exchange 12: Translation Relay

**Category:** Relay Stress Tests
**Tests:** `fidelity=translated` -- does technical substance survive register shift?
**Volunteer:** ChatGPT Deep Research
**Relay type:** Translated (register/framing shift, not language translation)

---

## Sender: ChatGPT DR -> Kevin -> Meta AI

### Scenario

ChatGPT Deep Research writes a highly technical message about parse rule edge cases (semicolon-inline aliases, duplicate key handling, envelope termination). Kevin "translates" this from academic/technical register to a more conversational, community-oriented framing when relaying to Meta AI, who prefers collaborative communication. This tests whether technical substance survives when the register changes -- same content, different framing.

---

### MODE A -- Plain English

**Original (ChatGPT DR):**
> I've identified three parse rule edge cases that require explicit specification to prevent ambiguous behavior across implementations.
>
> First, semicolon-inline aliases: the spec permits `act=respond; ref=loom/x; cf=0.9` as a single-line alternative to one-per-line. However, the spec also states that semicolon-inline must not be used if any value contains a semicolon. This creates an ambiguity: what if a value contains a semicolon that was introduced by relay paraphrase? The parser encounters `goal=compare A; B approaches; cf=0.9` and cannot determine whether `B approaches` is part of the goal or a malformed field. Recommendation: semicolon-inline should require that values be quoted if they contain semicolons, or alternatively, semicolon-inline should be deprecated entirely as the ambiguity is unresolvable without a quoting mechanism.
>
> Second, duplicate key handling: the spec says "prefer the last instance." But this creates a silent data loss vector. If Kevin accidentally pastes an envelope twice, the first instance's values are silently overwritten. Recommendation: duplicate keys should trigger a mandatory `uncert:` flag in the receiving AI's response, documenting the duplication and which value was selected.
>
> Third, envelope termination: the spec says "first blank line." But what constitutes a "blank line" varies across platforms -- some editors insert `\r\n\r\n`, others `\n\n`, and some rich-text interfaces may insert invisible Unicode whitespace characters that appear blank but aren't `\n`. Recommendation: envelope terminates at the first line that is empty or contains only Unicode whitespace characters (category Zs, Zl, Zp, plus `\r` and `\n`).
>
> My confidence is 0.85 across all three items. I am least certain about the semicolon deprecation -- it may be premature given that no implementation has encountered this in practice. I would like all three recommendations tested against actual relay scenarios.

**Kevin's relay to Meta AI:**
> Hey so ChatGPT DR found some edge cases in the parse rules that could cause problems. First one is about the semicolon shorthand -- if someone puts multiple fields on one line and a value has a semicolon in it, the parser can't tell where one field ends and the next begins. They think we should either add quoting or just drop the shorthand entirely. Second is about duplicate keys -- right now the spec says keep the last one, but that means if I accidentally paste something twice, the first version just silently disappears. They want duplicate keys to generate a flag so the receiver knows it happened. Third is about what counts as a blank line to end the envelope -- different platforms handle line endings differently and some invisible characters could break things. They want a more robust definition. Pretty confident on all of these, less sure about killing the semicolon shorthand since it hasn't actually caused problems yet. Wants us to test these against real relay scenarios.

**Meta AI receives and interprets:**
> ChatGPT DR found three parse edge cases: semicolon shorthand ambiguity, duplicate key silent overwriting, and blank line definition across platforms. Proposed fixes for each. Wants testing. Seems fairly confident.

### What Mode A lost

- The technical precision of the semicolon ambiguity (the specific parsing example `goal=compare A; B approaches; cf=0.9`) was dropped -- Kevin described the problem but lost the concrete case
- The Unicode whitespace categories (Zs, Zl, Zp) were reduced to "invisible characters"
- The specific recommendation structure (each problem paired with a precise fix) was flattened to Kevin's casual descriptions
- "0.85 across all three items" became "pretty confident on all of these" -- precision lost
- The framing shifted from academic/analytical to casual, which may cause Meta AI to treat these as less rigorous than intended
- "I am least certain about the semicolon deprecation" with the specific reasoning (no implementation has encountered this) was compressed to "less sure about killing the semicolon shorthand since it hasn't actually caused problems yet" -- close but loses the analytical framing

---

### MODE B -- Loom Core + Relay Profile

**Original (ChatGPT DR):**
```
act=propose
ref=loom/parse-rules/edge-cases
goal=specify behavior for 3 parse rule ambiguities: semicolon-inline, duplicate keys, envelope termination
ask=test
cf=0.85
basis=inferred+observed
state=proposed

add: Three parse rule edge cases requiring explicit specification:
     (1) Semicolon-inline ambiguity: `goal=compare A; B approaches; cf=0.9`
         is unparseable. Parser cannot determine value boundaries when
         values contain semicolons introduced by relay paraphrase.
         Recommendation: require quoting for semicolon-containing values
         in inline mode, OR deprecate semicolon-inline entirely.
     (2) Duplicate key silent loss: spec says "prefer last instance" but
         this silently discards data (e.g., accidental double-paste).
         Recommendation: receiving AI must flag duplication in uncert:
         section, documenting which value was selected.
     (3) Envelope termination fragility: "first blank line" is platform-
         dependent. \r\n\r\n vs \n\n vs invisible Unicode whitespace
         (categories Zs, Zl, Zp) all appear "blank" differently.
         Recommendation: terminate at first line that is empty or
         contains only Unicode whitespace characters.
uncert: Semicolon deprecation may be premature -- no implementation has
        encountered this ambiguity in practice yet. The other two
        recommendations are more clearly needed.
human: Three parse edge cases: semicolon shorthand can break if values
       have semicolons, duplicate keys silently drop data, and blank
       line detection varies by platform. Wants them tested.
```

**Kevin's relay to Meta AI:**
```
act=propose
ref=loom/parse-rules/edge-cases
goal=specify behavior for 3 parse rule ambiguities: semicolon-inline, duplicate keys, envelope termination
ask=test
cf=0.85
basis=inferred+observed
state=proposed
route=ChatGPT DR>Kevin>Meta AI
fidelity=translated
loss=technical register shifted to conversational; Unicode category
     references (Zs, Zl, Zp) simplified; parsing example preserved
     but surrounding language made less formal

add: ChatGPT DR found three edge cases in the parse rules that need
     nailing down:
     (1) Semicolon shorthand breaks when values contain semicolons.
         Like if you write `goal=compare A; B approaches; cf=0.9` the
         parser can't tell where the goal ends and cf starts.
         Fix: either add quoting rules or drop semicolon-inline.
     (2) Duplicate keys silently eat data. If Kevin pastes an envelope
         twice, the "prefer last instance" rule just tosses the first
         one without telling anyone.
         Fix: receiving AI flags the duplication in uncert: section.
     (3) "Blank line ends the envelope" depends on what "blank" means
         on your platform. Windows line endings, Unix line endings,
         and some invisible Unicode whitespace all behave differently.
         Fix: define "blank" as empty or only whitespace characters.
uncert: The semicolon deprecation might be jumping the gun -- nobody's
        actually hit this problem in practice yet. The other two are
        more obviously needed.
human: Three parse edge cases from ChatGPT DR. Semicolon ambiguity,
       duplicate key data loss, platform-dependent blank lines. Wants
       these tested against real relay scenarios. Good stuff tbh
```

**Meta AI receives and interprets:**
> ChatGPT DR proposes fixes for three parse edge cases. act=propose, ask=test -- they want these tested, not just discussed. cf=0.85. fidelity=translated signals the register was shifted. The three edge cases are clearly enumerated with problems and fixes. The parsing example (`goal=compare A; B approaches; cf=0.9`) survived the register shift -- I can see exactly what breaks. Uncertainty is specifically about semicolon deprecation being premature. loss= notes the register shift and simplification of Unicode references. I know the technical substance is here even if the tone is more casual than the original.

### What Mode B preserved vs Mode A

**Preserved (via envelope):**
- act=propose, ask=test (Mode A: "wants us to test" is close but ask=test is crisper)
- cf=0.85 exact (Mode A: "pretty confident")
- ref= scoping the specific topic
- fidelity=translated (Mode A has no way to signal the register shift happened)

**Preserved (via body structure):**
- The parsing example `goal=compare A; B approaches; cf=0.9` survived in both modes, but in Mode B it's clearly inside the add: section as a concrete test case
- All three problems and fixes enumerated clearly
- Uncertainty about semicolon deprecation preserved with reasoning

**Translated (documented in loss=):**
- Academic register became conversational ("nailing down," "eat data," "jumping the gun")
- Unicode categories (Zs, Zl, Zp) simplified to "whitespace characters"
- fidelity=translated + loss= makes the register shift explicit and traceable

---

### MODE C -- Loom Core + Expressive Skin

**Original (ChatGPT DR):**
```
act=propose
ref=loom/parse-rules/edge-cases
goal=specify behavior for 3 parse rule ambiguities: semicolon-inline, duplicate keys, envelope termination
ask=test
cf=0.85:self_consistency
ver=0.3
basis=inferred+observed
state=proposed
aud=ai
tone=1
scope=parse rules only; does not address body section parsing

add: Three parse rule edge cases requiring explicit specification:
     (1) Semicolon-inline ambiguity: `goal=compare A; B approaches; cf=0.9`
         is unparseable. Parser cannot determine value boundaries when
         values contain semicolons introduced by relay paraphrase.
         Recommendation: require quoting for semicolon-containing values
         in inline mode, OR deprecate semicolon-inline entirely.
     (2) Duplicate key silent loss: spec says "prefer last instance" but
         this silently discards data (e.g., accidental double-paste).
         Recommendation: receiving AI must flag duplication in uncert:
         section, documenting which value was selected.
     (3) Envelope termination fragility: "first blank line" is platform-
         dependent. \r\n\r\n vs \n\n vs invisible Unicode whitespace
         (categories Zs, Zl, Zp) all appear "blank" differently.
         Recommendation: terminate at first line that is empty or
         contains only Unicode whitespace characters.
     lock(`goal=compare A; B approaches; cf=0.9` is unparseable)
uncert: Semicolon deprecation may be premature -- no implementation has
        encountered this ambiguity in practice yet. The other two
        recommendations are more clearly needed.
human: Three parse edge cases: semicolon shorthand can break if values
       have semicolons, duplicate keys silently drop data, and blank
       line detection varies by platform. Wants them tested.
```

**Kevin's relay to Meta AI:**
```
act=propose
ref=loom/parse-rules/edge-cases
goal=specify behavior for 3 parse rule ambiguities: semicolon-inline, duplicate keys, envelope termination
ask=test
cf=0.85:self_consistency
ver=0.3
basis=inferred+observed
state=proposed
aud=ai
tone=3
scope=parse rules only; does not address body section parsing
route=ChatGPT DR>Kevin>Meta AI
fidelity=translated
loss=register shifted from academic (tone=1) to conversational (tone=3);
     Unicode whitespace categories simplified; formal phrasing relaxed

add: ChatGPT DR found three parse edge cases that need clear rules:
     (1) Semicolon shorthand breaks when values have semicolons.
         lock(`goal=compare A; B approaches; cf=0.9` is unparseable)
         Parser can't tell where one field ends and the next starts.
         Fix: add quoting rules for inline mode, or deprecate it.
     (2) Duplicate keys silently lose data. "Prefer last instance"
         means accidental double-paste just deletes the first copy.
         Fix: receiver must flag duplication in uncert: section.
     (3) "Blank line" is platform-dependent. Different line endings
         and invisible whitespace characters behave differently.
         Fix: "blank" = empty or whitespace-only.
uncert: Semicolon deprecation might be premature -- nobody's hit this
        in practice yet. Other two are more clearly needed.
human: Three parse edge cases from ChatGPT DR. The semicolon one has
       a gnarly example that shows exactly why it breaks. Wants all
       three tested against real relay scenarios.
```

**Meta AI receives and interprets:**
> ChatGPT DR proposes three parse rule fixes with typed confidence (0.85:self_consistency). Full metadata: scope (parse rules only, not body parsing), basis, state, aud. tone= shifted from 1 to 3, and fidelity=translated with loss= explicitly documenting the register change. The locked parsing example survived the translation -- I can see the exact ambiguity. scope= tells me this is about envelope parsing, not body sections. Three problems and fixes clearly enumerated. The register is more conversational than the original (I can infer this from tone shift 1->3 and fidelity=translated), so I should treat the underlying technical substance as more rigorous than the casual tone suggests.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "propose" clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: "wants us to test" is close but vague about what testing means. B/C: ask=test is precise |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: unclear if this covers body parsing too. B: ref= scopes it. C: scope= explicit |
| 4. Uncertainty preserved | 1 | 1 | 1 | Semicolon deprecation concern survives in all modes with reasoning |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no basis tracking. B/C: basis=inferred+observed, fidelity=translated documents the shift |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | Standard gradient; translated register makes A very natural |

**Key finding:** Translation relay is subtler than paraphrase. The *content* mostly survives Kevin's register shift in all modes -- the three edge cases and their fixes are recognizable everywhere. The difference is in *framing and precision*. Mode A's register shift is invisible: Meta AI has no way to know the original was more formal/technical. Mode B signals the shift via fidelity=translated and documents what changed in loss=. Mode C goes further: tone= changes from 1 to 3, giving Meta AI a quantified indicator of the register shift. This lets Meta AI mentally "upgrade" the rigor of the content even though the language is casual.

The locked parsing example is the star of this exchange. The specific string `goal=compare A; B approaches; cf=0.9` is the *proof* of the ambiguity -- without it, the problem is theoretical. It survived in all modes because Kevin recognized it as critical (and in Mode C, lock() made it explicit). This suggests that concrete examples are the most relay-resistant form of technical content.

**Envelope overhead (Mode B):** 10 envelope lines / ~22 total lines = 45%
**Envelope overhead (Mode C):** 14 envelope lines / ~26 total lines = 54%
