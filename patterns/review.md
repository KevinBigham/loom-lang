# Pattern: review

**Name:** `pattern=review`
**Status:** Core (ships with v0.3)
**Proposed by:** ChatGPT (stance-based body format)

## Description

The default Loom body pattern for structured responses. Forces the responder to categorize every piece of their response by its relationship to prior messages.

## Body sections (in order)

| Section | Required? | Purpose |
|---------|-----------|---------|
| `quote:` | No | Exact cited content (implicitly locked) |
| `adopt:` | No | What you endorse |
| `add:` | No | New contributions |
| `change:` | No | Modifications to existing ideas |
| `uncert:` | No | Where you're unsure |
| `challenge:` | No | Disagreements (must include `reason:` + alternative) |
| `human:` | Recommended | One-sentence plain-language summary |

## Example

```
act=respond
ref=loom/naming
goal=review naming proposals and cast vote
ask=decide
cf=0.85
pattern=review

adopt: "Loom" is the right name — evocative and scalable.
add: Consider "Loom Core Protocol" as the formal spec name.
change: Drop "AIOL" from user-facing documentation.
uncert: Not sure if "Core" is needed in the name at all.
human: I vote for Loom. Keep it simple.
```
