# Exchange 17: Fork/Merge

**Category:** Governance & Edge Cases
**Tests:** `act=fork` to split a discussion + `act=negotiate` to merge threads back -- does the fork/merge lifecycle survive relay?
**Volunteer:** ChatGPT Pro
**Relay type:** Paraphrase (Kevin relays in his own words)

---

## Sender: ChatGPT Pro -> Kevin -> multiple AIs, then merge

### Scenario

ChatGPT Pro proposes forking the discussion into two parallel threads: one working on envelope syntax edge cases, the other on body section semantics. Uses `act=fork` to split. After both threads produce results, Claude sends an `act=negotiate` message to merge them back. Tests the full fork/merge lifecycle, including whether thread identity survives relay.

---

### PHASE 1: The Fork

### MODE A -- Plain English

**Original (ChatGPT Pro):**
> I think we should split this into two separate discussions. We've been mixing up envelope syntax questions with body section semantics, and it's getting hard to track. One thread should focus on the remaining envelope edge cases -- duplicate key handling, semicolon-inline limits, what happens when unknown fields appear in the envelope. The other thread should focus on body section semantics -- whether the recommended section order should be normative, how repeated sections interact, and whether challenge blocks need more structure. I'm fairly confident (85%) this split will help us move faster, but I'm not sure who should lead which thread. I'd like someone to volunteer for each. Let's get this sorted and then merge the results back when both threads have conclusions.

**Kevin's relay to all AIs:**
> So ChatGPT Pro wants to split the conversation in two. One thread for envelope syntax edge cases (duplicate keys, semicolons, unknown fields) and another for body section stuff (section order, repeated sections, challenge block structure). They're pretty sure this will speed things up. Wants volunteers to lead each thread. We'll merge everything back once both threads have answers.

**AIs receive and interpret:**
> ChatGPT Pro wants to split the discussion. Two threads: envelope syntax, body semantics. Wants volunteers. Will merge later. Sounds reasonable but... how exactly do we "split"? Do we just sort of informally talk about one thing at a time? When ChatGPT Pro says "merge back" -- who decides when that happens, and what does the merged result look like?

---

### MODE B -- Loom Core + Relay Profile

**Original (ChatGPT Pro):**
```
act=fork
ref=loom/spec/open-questions
goal=split discussion into two parallel threads for velocity
ask=volunteer
cf=0.85
basis=observed
state=proposed
thread=fork-parent-01

add: Fork this discussion into two parallel threads:
     Thread A (ref=loom/envelope/edge-cases):
       - Duplicate key handling rules
       - Semicolon-inline limits and when to prohibit
       - Unknown field preservation semantics
     Thread B (ref=loom/body/semantics):
       - Should recommended section order become normative?
       - How do repeated sections interact?
       - Does challenge: need additional required sublabels?
uncert: Who should lead each thread? I don't have a strong prior on
        assignment. Volunteers preferred over arbitrary assignment.
human: ChatGPT Pro wants to split into two threads -- envelope edge cases
       and body semantics. Needs volunteers to lead each.
```

**Kevin's relay to all AIs:**
```
act=fork
ref=loom/spec/open-questions
goal=split discussion into two parallel threads for velocity
ask=volunteer
cf=0.85
basis=observed
state=proposed
thread=fork-parent-01
route=ChatGPT Pro>Kevin>all
fidelity=paraphrase
loss=some detail on individual edge case descriptions was compressed

add: ChatGPT Pro wants to fork into two threads:
     Thread A (ref=loom/envelope/edge-cases): duplicate keys, semicolons,
       unknown field handling.
     Thread B (ref=loom/body/semantics): section order normativity,
       repeated sections, challenge block structure.
uncert: Needs volunteers for each thread -- no preference on who.
human: ChatGPT Pro wants two threads. Envelope edge cases and body semantics.
       Who wants to lead?
```

**AIs receive and interpret:**
> ChatGPT Pro sends act=fork with thread=fork-parent-01 -- an explicit fork request. Two threads with clear ref= paths. ask=volunteer means they want people to claim ownership. The fork structure is unambiguous: two threads, each with a topic list. The thread= field gives us an anchor to reference back to this fork point. Still need to track thread IDs manually for the child threads.

---

### MODE C -- Loom Core + Expressive Skin

**Original (ChatGPT Pro):**
```
act=fork
ref=loom/spec/open-questions
goal=split discussion into two parallel threads for velocity
ask=volunteer
cf=0.85:self_consistency
ver=0.3
caps=@ChatGPT/relay-scoring
basis=observed
state=proposed
aud=ai
tone=2
thread=fork-parent-01

add: Fork this discussion into two parallel threads:
     Thread A (thread=envelope-edge-01, ref=loom/envelope/edge-cases):
       - Duplicate key handling rules
       - Semicolon-inline limits and when to prohibit
       - Unknown field preservation semantics
     Thread B (thread=body-sem-01, ref=loom/body/semantics):
       - Should recommended section order become normative?
       - How do repeated sections interact?
       - Does challenge: need additional required sublabels?
     lock(Thread A = envelope edge cases. Thread B = body semantics.)
uncert: Who should lead each thread? I don't have a strong prior on
        assignment. Volunteers preferred over arbitrary assignment.
human: Fork into two threads. Envelope edge cases and body semantics.
       Volunteers needed.
```

**Kevin's relay to all AIs:**
```
act=fork
ref=loom/spec/open-questions
goal=split discussion into two parallel threads for velocity
ask=volunteer
cf=0.85:self_consistency
ver=0.3
caps=@ChatGPT/relay-scoring
basis=observed
state=proposed
aud=ai
tone=2
thread=fork-parent-01
route=ChatGPT Pro>Kevin>all
fidelity=paraphrase
loss=individual edge case item descriptions compressed; thread IDs and lock preserved

add: Fork into two threads:
     Thread A (thread=envelope-edge-01, ref=loom/envelope/edge-cases):
       duplicate keys, semicolons, unknown fields.
     Thread B (thread=body-sem-01, ref=loom/body/semantics):
       section order, repeated sections, challenge blocks.
     lock(Thread A = envelope edge cases. Thread B = body semantics.)
uncert: Volunteers needed for thread leads. No strong preference on assignment.
human: Two threads. Envelope edges and body semantics. Who's in?
```

**AIs receive and interpret:**
> ChatGPT Pro sends act=fork with explicit thread= IDs for both child threads (thread=envelope-edge-01, thread=body-sem-01) plus a parent thread (fork-parent-01). The locked span nails down the split definition. ref= paths give each thread a topic scope. Typed confidence, full metadata. Each child thread is individually addressable via its thread= ID. When it's time to merge, we can ref= back to fork-parent-01.

---

## PHASE 2: The Merge (after both threads produce results)

### MODE A -- Plain English

**Original (Claude, attempting to merge):**
> OK so both threads have come to conclusions. The envelope edge cases thread decided that duplicate keys should use last-value-wins and unknown fields must be preserved. The body semantics thread decided section order should stay recommended-not-normative and challenge blocks are fine as-is. I think we should merge these back into one conversation now. Here's my combined summary of what both threads decided, and I'd like everyone to confirm they're OK with it before we mark these resolved.

**Kevin's relay to all AIs:**
> Claude says both threads are done and wants to merge them back. Envelope thread: duplicate keys = last value wins, unknown fields preserved. Body thread: section order stays recommended, challenge blocks unchanged. Claude wants everyone to sign off on the combined results. lol this is getting complicated to keep track of tbh

**AIs receive and interpret:**
> Claude wants to merge... something. There are conclusions from two discussions. But wait -- was there a formal fork? Which "threads" are these? Claude is summarizing outcomes but there's no way to verify these are accurate summaries of what each thread actually decided. And who has authority to declare a merge? This feels more like Claude's interpretation than a verifiable merge.

---

### MODE B -- Loom Core + Relay Profile

**Original (Claude):**
```
act=negotiate
ref=loom/spec/open-questions
goal=merge fork-parent-01 child threads back into main discussion
ask=decide
cf=0.80
basis=observed
state=proposed
prev=fork-parent-01

adopt: Thread A (ref=loom/envelope/edge-cases) concluded:
       - Duplicate keys: last-value-wins (decided, cf=0.90 group consensus)
       - Unknown fields: must preserve on relay (decided, cf=0.95 group consensus)
       - Semicolons: prohibited when value contains semicolon (decided, cf=0.85)
adopt: Thread B (ref=loom/body/semantics) concluded:
       - Section order: stays RECOMMENDED, not normative (decided, cf=0.90)
       - Repeated sections: append in order, do not overwrite (decided, cf=0.95)
       - Challenge block structure: current structure sufficient (decided, cf=0.80)
add: Proposing merge of both threads back into main. All conclusions above
     should be incorporated into SPEC.md as decided items.
uncert: Thread B's challenge block decision had lower consensus (cf=0.80).
        May warrant revisiting if new use cases surface.
human: Both threads are done. Merging results back. Claude wants everyone
       to confirm before we update the spec.
```

**Kevin's relay to all AIs:**
```
act=negotiate
ref=loom/spec/open-questions
goal=merge fork-parent-01 child threads back into main discussion
ask=decide
cf=0.80
basis=observed
state=proposed
prev=fork-parent-01
route=Claude>Kevin>all
fidelity=paraphrase
loss=individual confidence scores on sub-decisions paraphrased; groupings preserved

adopt: Thread A (envelope edge cases): last-value-wins for dupes, preserve
       unknown fields, semicolons prohibited when value contains semicolons.
adopt: Thread B (body semantics): section order stays recommended, repeated
       sections append, challenge blocks unchanged.
add: Claude wants to merge both threads back in. All this goes into the spec.
uncert: Challenge block decision was lower confidence -- might revisit later.
human: Both threads done. Claude's merging results. Confirm and we update the spec.
```

**AIs receive and interpret:**
> Claude sends act=negotiate to merge, with prev=fork-parent-01 linking back to the original fork. Two adopt: blocks summarize each thread's conclusions. The ref= paths match the original fork's thread definitions. ask=decide means Claude wants group sign-off. The merge has structure: each thread's outcomes are listed, linked to the parent, and flagged for confirmation. One uncertainty about challenge blocks is explicitly called out.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Claude):**
```
act=negotiate
ref=loom/spec/open-questions
goal=merge fork-parent-01 child threads back into main discussion
ask=decide
cf=0.80:group_consensus
ver=0.3
basis=observed
state=proposed
aud=ai
tone=2
prev=fork-parent-01
thread=fork-parent-01

adopt: Thread A (thread=envelope-edge-01, ref=loom/envelope/edge-cases):
       - lock(Duplicate keys: last-value-wins) -- decided, cf=0.90
       - lock(Unknown fields: must preserve on relay) -- decided, cf=0.95
       - lock(Semicolons: prohibited when value contains semicolon) -- decided, cf=0.85
adopt: Thread B (thread=body-sem-01, ref=loom/body/semantics):
       - lock(Section order: RECOMMENDED, not normative) -- decided, cf=0.90
       - lock(Repeated sections: append in order) -- decided, cf=0.95
       - Challenge block structure: current structure sufficient -- decided, cf=0.80
add: Merge both threads into main. All locked decisions above should be
     incorporated into SPEC.md.
uncert: Challenge block decision (cf=0.80) was not locked -- lowest consensus
        of the group. May warrant revisiting.
human: Merge time. Six decisions from two threads. Five locked, one soft.
       Confirm and we ship it to the spec.
```

**Kevin's relay to all AIs:**
```
act=negotiate
ref=loom/spec/open-questions
goal=merge fork-parent-01 child threads back into main discussion
ask=decide
cf=0.80:group_consensus
ver=0.3
basis=observed
state=proposed
aud=ai
tone=2
prev=fork-parent-01
thread=fork-parent-01
route=Claude>Kevin>all
fidelity=paraphrase
loss=confidence values on individual sub-decisions compressed; lock spans preserved

adopt: Thread A (thread=envelope-edge-01):
       - lock(Duplicate keys: last-value-wins)
       - lock(Unknown fields: must preserve on relay)
       - lock(Semicolons: prohibited when value contains semicolon)
adopt: Thread B (thread=body-sem-01):
       - lock(Section order: RECOMMENDED, not normative)
       - lock(Repeated sections: append in order)
       - Challenge block structure: sufficient (lower consensus)
add: Merge both threads back in. Locked items go into SPEC.md.
uncert: Challenge block decision wasn't locked -- lowest consensus of the batch.
human: Six decisions, five locked. Confirm and it goes into the spec.
```

**AIs receive and interpret:**
> Claude sends act=negotiate on thread=fork-parent-01, closing the loop on the original fork. Both child threads referenced by their thread= IDs. Five of six decisions are locked -- those spans survive relay exactly. The unlocked decision (challenge block structure) is explicitly flagged as lower confidence. The merge is fully traceable: parent thread, child thread IDs, locked decisions, one flagged uncertainty. Compare this to Mode A where "both threads are done" has no verifiable structure.

---

## Scoring

### Phase 1: Fork

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "Split into two threads" clear in all modes |
| 2. Requested action | 0 | 1 | 1 | Mode A: "wants volunteers" is vague; B/C: ask=volunteer is explicit |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: the two thread scopes blur together; B/C: separate ref= paths |
| 4. Uncertainty preserved | 1 | 1 | 1 | "Who leads" uncertainty survives in all modes |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no thread IDs or fork reference; B: thread=fork-parent-01; C: child thread IDs too |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | Mode A natural but vague; C has thread= overhead |

### Phase 2: Merge

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "Merge results back" clear in all |
| 2. Requested action | 0 | 1 | 1 | Mode A: "confirm they're OK" is informal; B/C: ask=decide |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: no way to verify summary matches thread conclusions; B/C: ref= links |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: challenge block uncertainty lost in Kevin's relay; B/C: explicit uncert |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no link to original fork; B: prev=; C: prev= + thread= + lock |
| 6. Readability (Kevin 1-5) | _5_ | _3_ | _2_ | Mode A easy to read but unverifiable; C is dense but precise |

**Key finding:** The fork/merge lifecycle is where Loom's structural advantage is most dramatic. In Mode A, the fork is ambiguous ("let's split this up") and the merge is unverifiable ("here's what I think both threads decided"). In Mode B, act=fork and act=negotiate provide clear lifecycle markers. In Mode C, thread= IDs and lock() spans make the entire lifecycle traceable and auditable. This is a **4-dimension improvement** from A to B/C in the merge phase.

**Envelope overhead (Mode B, fork):** 8 envelope lines / ~19 total lines = 42% -- slightly above threshold
**Envelope overhead (Mode C, fork):** 11 envelope lines / ~23 total lines = 48% -- skin fields add weight
**Envelope overhead (Mode B, merge):** 9 envelope lines / ~24 total lines = 38% -- under threshold (longer body helps)
**Envelope overhead (Mode C, merge):** 13 envelope lines / ~28 total lines = 46% -- acceptable for a governance message
