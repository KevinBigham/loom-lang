# Loom v0.3 Validation Checklist

Use this checklist to verify any Loom message is well-formed before relay or scoring.

## Envelope

- [ ] All required fields present: `act`, `ref`, `goal`, `ask`, `cf`
- [ ] Envelope is key=value, one per line
- [ ] Envelope terminates at first blank line
- [ ] Key = text before first `=`; value = text after first `=`
- [ ] No duplicate keys (if present, last instance wins; flag in `uncert:`)
- [ ] `act` value is one of: propose, query, respond, refine, challenge, affirm, riff, handoff, fork, negotiate
- [ ] `ask` value is one of: critique, extend, merge, decide, test, acknowledge, volunteer, none
- [ ] `cf` is 0.00-1.00, optionally typed (e.g., `cf=0.85:self_consistency`)

## Body

- [ ] Body begins after blank line following envelope
- [ ] Section labels from: quote, adopt, add, change, uncert, challenge, human
- [ ] Sections appear in recommended order (quote > adopt > add > change > uncert > challenge > human)
- [ ] `challenge:` includes `reason:` sublabel and alternative or question
- [ ] `human:` is one sentence, plain language
- [ ] `quote:` content is verbatim (implicitly locked)
- [ ] Repeated section labels append in order, do not overwrite
- [ ] `lock(...)` spans are not nested

## Relay

- [ ] Unknown envelope fields preserved (not dropped)
- [ ] If `fidelity` != `exact`: `quote:` content was not silently converted to `adopt:`
- [ ] If `loss` is non-empty: `cf` did not increase during relay
- [ ] `route` reflects actual relay path
- [ ] `fidelity` accurately describes relay type (exact/paraphrase/abridged/translated/enriched)

## Extensions

- [ ] Typed payload blocks use `[[type:...]]` followed by fenced code block
- [ ] `caps=` lists supported extension namespaces (comma-separated)
- [ ] @Gemini/Topo nesting depth <= 3 unless explicitly overridden
