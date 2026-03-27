# Loom Spec Drift Queue

Track mismatches between the published spec, grammar appendix, examples, and observed usage here. Do not bury drift inside ad hoc edits.

## How to Use This Queue

- Add a new item when live usage, parser work, or benchmark review reveals a mismatch.
- Link real-world evidence from [`corpus/`](../corpus/README.md) whenever possible.
- Assign each item to the milestone where it must be resolved.
- Do not force resolution early if the project still needs field pressure.

## Seeded Drift Items

| ID | Title | Source | Impact | Target | Status |
|----|-------|--------|--------|--------|--------|
| `drift-001` | ~~ABNF header described as v0.3~~ | [`grammar/ABNF.md`](../grammar/ABNF.md) | Resolved: updated to v0.4. | `v0.5` | **Closed** |
| `drift-002` | ~~ABNF body-section grammar missing `enrich:`~~ | [`grammar/ABNF.md`](../grammar/ABNF.md), [`SPEC.md`](../SPEC.md) | Resolved: `enrich` added to section-label rule + section order comment. | `v0.5` | **Closed** |
| `drift-003` | Observed values appear in the appendix but not in the spec enums (`basis=designed`, `basis=computed`, `state=active`, `aud=all`) | [`grammar/ABNF.md`](../grammar/ABNF.md), benchmark exchanges | Parser work will need a decision on whether these are valid expansions or non-conformant examples. | `v0.7` | Open |
| `drift-004` | Note [E] appears to conflate `basis` values with a confidence type (`self-awareness`) | [`grammar/ABNF.md`](../grammar/ABNF.md) | This is a misleading grammar note and will confuse any future normative freeze. | `v0.5` | Open |
| `drift-005` | Blank-line termination is still underspecified for parser-grade implementations | [`SPEC.md`](../SPEC.md), [`grammar/ABNF.md`](../grammar/ABNF.md), benchmark exchange 12 | Interop work needs a crisper definition for LF/CRLF and whitespace-only lines. | `v0.7` | Open |
| `drift-006` | Semicolon-inline remains allowed, but quoting/escaping behavior is still unresolved | [`SPEC.md`](../SPEC.md), benchmark exchange 12 | Parser/validator behavior will diverge unless the project either tightens or de-emphasizes inline form. | `v0.7` | Open |

## Resolution Rule

An item is closed only when the repo contains both:

- the deciding evidence or rationale
- the document change that resolves the mismatch
