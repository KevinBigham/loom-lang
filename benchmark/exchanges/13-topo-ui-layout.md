# Exchange 13: Topo-Layer UI Layout

**Category:** Extension & Dialect Tests
**Tests:** Spatial layout using @Gemini/Topo notation -- do bounding boxes and encapsulation survive relay?
**Volunteer:** Gemini
**Relay type:** Paraphrase

---

## Sender: Gemini -> Kevin -> Claude

### MODE A -- Plain English

**Original (Gemini):**
> I've been thinking about the dashboard layout for the mobile app. Here's what I have in mind. At the very top, there's a fixed header bar that spans the full width -- 360 pixels wide and 56 pixels tall. It contains the app logo on the left and a settings gear icon on the right. Below that, the main content area is split into two columns. The left column is a sidebar navigation panel, 96 pixels wide and taking up the remaining height (let's say 640 pixels to fill the screen minus the header and bottom bar). It contains vertically stacked nav icons. The right column is the main content panel, 264 pixels wide and the same 640 pixels tall, where the actual dashboard cards and data live. At the very bottom, there's a fixed action bar, again full width at 360 by 56 pixels, with three action buttons evenly spaced. The sidebar is contained within the main content area, not floating independently -- it's part of that two-column split. I'm about 85% confident this is the right structure, but I'm not sure whether the sidebar should be collapsible on smaller screens. I'd like your critique on whether this layout holds up.

**Kevin's relay to Claude:**
> Gemini has a dashboard layout for the mobile app. There's a header bar at the top, full width, with a logo and settings icon. Then two columns underneath -- a narrow sidebar on the left with nav icons and a wider main content area on the right for dashboard cards. Bottom has an action bar with three buttons. They're pretty confident but not sure about making the sidebar collapsible. Want your critique.

**Claude receives and interprets:**
> Gemini proposes a two-column mobile dashboard with header, sidebar, main content, and bottom action bar. Specific dimensions were not communicated. The nesting relationship (sidebar inside the content area vs. independent) is unclear. Wants my critique. The collapsibility question was relayed but without the specific dimensional context that would inform the answer.

---

### MODE B -- Loom Core + Relay Profile

**Original (Gemini):**
```
act=propose
ref=app/mobile/dashboard-layout
goal=establish dashboard layout: header + 2-col body (sidebar|main) + action bar
ask=critique
cf=0.85
basis=designed
state=proposed

add: Dashboard layout for 360px-wide mobile viewport (total height 752px):
     - Header bar: 360x56px, fixed top. Logo left-aligned, settings icon right.
     - Content area: 360x640px, split into two columns:
       * Sidebar nav: 96x640px, left. Vertically stacked nav icons.
       * Main panel: 264x640px, right. Dashboard cards and data.
       Sidebar is nested INSIDE the content area, not independent.
     - Action bar: 360x56px, fixed bottom. Three buttons, evenly spaced.

uncert: Should sidebar be collapsible on screens narrower than 360px?
        Unsure if 96px sidebar is too wide for small viewports.
human: I designed a mobile dashboard -- header, two-column middle (sidebar + main),
       and a bottom action bar. Want your thoughts.
```

**Kevin's relay to Claude:**
```
act=propose
ref=app/mobile/dashboard-layout
goal=establish dashboard layout: header + 2-col body (sidebar|main) + action bar
ask=critique
cf=0.85
route=Gemini>Kevin>Claude
fidelity=paraphrase
loss=exact pixel dimensions for all regions; nesting relationship may be imprecise

add: Gemini designed a mobile dashboard layout:
     - Header bar at top, full width, with logo and settings icon.
     - Two-column content area: narrow sidebar on the left for nav icons,
       wider main panel on the right for dashboard cards.
     - Action bar at bottom with three buttons.
uncert: Not sure if sidebar should be collapsible on smaller screens.
human: Gemini has a mobile dashboard layout -- header, sidebar + main content, bottom bar.
       Wants your critique.
```

**Claude receives and interprets:**
> Gemini proposes a mobile dashboard with header, two-column body, and action bar. act=propose, ask=critique -- they want structural feedback. cf=0.85 is fairly confident. Pixel dimensions were lost per the loss field, so I can't evaluate proportions precisely. The nesting relationship is stated but I can see from the loss field that it may be imprecise. Uncertainty about sidebar collapsibility is clear.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Gemini):**
```
act=propose
ref=app/mobile/dashboard-layout
goal=establish dashboard layout: header + 2-col body (sidebar|main) + action bar
ask=critique
cf=0.85:design_confidence
ver=0.3
caps=@Gemini/Topo
basis=designed
state=proposed
aud=ai
tone=2

add: Mobile dashboard, 360px viewport.

     [UI: header | 360x56 | fixed-top]
       << logo: left-aligned
       << settings-icon: right-aligned

     [UI: content-area | 360x640 | below header]
       << [UI: sidebar-nav | 96x640 | left]
            << nav-icons: vertical-stack
       << [UI: main-panel | 264x640 | right]
            << dashboard-cards: flow-layout

     [UI: action-bar | 360x56 | fixed-bottom]
       << btn-1: left-third
       << btn-2: center-third
       << btn-3: right-third

     ASCII fallback:
     +--[header 360x56]------------------+
     | logo               settings-icon  |
     +----+-------------------------------+
     |side|  main-panel 264x640          |
     | 96 |  [dashboard cards]           |
     | nav|                              |
     |icons                              |
     +----+-------------------------------+
     +--[action-bar 360x56]--------------+
     | [btn-1]   [btn-2]   [btn-3]      |
     +------------------------------------+

uncert: Should sidebar collapse below 360px width?
        96px sidebar = 26.7% of viewport -- possibly too greedy.
human: Mobile dashboard layout with Topo notation and an ASCII diagram.
       Want your critique on the structure.
```

**Kevin's relay to Claude:**
```
act=propose
ref=app/mobile/dashboard-layout
goal=establish dashboard layout: header + 2-col body (sidebar|main) + action bar
ask=critique
cf=0.85:design_confidence
ver=0.3
caps=@Gemini/Topo
basis=designed
state=proposed
aud=ai
tone=2
route=Gemini>Kevin>Claude
fidelity=paraphrase
loss=Topo [UI:] blocks copied as-is; I don't fully grok the notation but the ASCII diagram makes sense

add: Mobile dashboard, 360px viewport.

     [UI: header | 360x56 | fixed-top]
       << logo: left-aligned
       << settings-icon: right-aligned

     [UI: content-area | 360x640 | below header]
       << [UI: sidebar-nav | 96x640 | left]
            << nav-icons: vertical-stack
       << [UI: main-panel | 264x640 | right]
            << dashboard-cards: flow-layout

     [UI: action-bar | 360x56 | fixed-bottom]
       << btn-1: left-third
       << btn-2: center-third
       << btn-3: right-third

     ASCII fallback:
     +--[header 360x56]------------------+
     | logo               settings-icon  |
     +----+-------------------------------+
     |side|  main-panel 264x640          |
     | 96 |  [dashboard cards]           |
     | nav|                              |
     |icons                              |
     +----+-------------------------------+
     +--[action-bar 360x56]--------------+
     | [btn-1]   [btn-2]   [btn-3]      |
     +------------------------------------+

uncert: Should sidebar collapse below 360px? 96px is about 27% of the viewport.
human: Gemini's mobile dashboard layout. The box notation is Gemini's spatial thing --
       the ASCII art at the bottom shows the same layout in plain text.
```

**Claude receives and interprets:**
> Gemini proposes a mobile dashboard layout using @Gemini/Topo notation (caps confirms support). Full spatial structure preserved: header 360x56 fixed-top, two-column content area with 96px sidebar and 264px main panel, action bar 360x56 fixed-bottom. The << encapsulation shows nesting clearly -- sidebar and main panel are children of content-area. ASCII fallback confirms the layout visually. Kevin copied the Topo blocks verbatim even though he didn't fully understand the notation (per his loss field note), which is exactly the relay pattern the protocol is designed for. cf=0.85:design_confidence, uncertainty about sidebar collapsibility at 26.7% viewport width.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "propose" clear in all modes |
| 2. Requested action | 1 | 1 | 1 | "critique" / ask=critique preserved in all |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: lost pixel dimensions, nesting ambiguous ("two columns" doesn't convey 96/264 split or containment) |
| 4. Uncertainty preserved | 1 | 1 | 1 | Collapsibility question survived all modes |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no basis; B/C: basis=designed |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _3_ | A is natural; B is structured prose; C has Topo notation that Kevin copied without fully understanding |

**Key finding:** The critical spatial difference is in scope (dimension 3). Mode A's "narrow sidebar on the left" lost the 96/264 pixel split and the explicit nesting. Mode C's Topo notation survived relay because Kevin could copy it even without understanding the `[UI:]` and `<<` syntax -- the ASCII fallback gave him enough confidence that the notation was worth preserving.

**Envelope overhead (Mode B):** 7 envelope lines / ~20 total lines = 35%
**Envelope overhead (Mode C):** 12 envelope lines / ~40 total lines = 30% (longer body dilutes overhead)
