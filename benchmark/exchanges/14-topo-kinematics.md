# Exchange 14: Topo-Layer Kinematic Physics

**Category:** Extension & Dialect Tests
**Tests:** Kinematic/vector data using @Gemini/Topo v[...] notation -- does physics survive paraphrase relay?
**Volunteer:** Gemini
**Relay type:** Paraphrase

---

## Sender: Gemini -> Kevin -> DeepSeek

### MODE A -- Plain English

**Original (Gemini):**
> I've been modeling a bouncing ball simulation for the physics demo. Here's the setup. The ball starts at position x=50, y=700 (near the bottom-left of an 800x800 canvas). It has an initial velocity of 3 units per frame to the right and 12 units per frame upward (so it launches up and to the right). Gravity pulls it down at 0.4 units per frame squared. When the ball hits the floor (y=800), it bounces with a restitution coefficient of 0.75 -- meaning it retains 75% of its vertical speed on each bounce, with the vertical component reversed. Horizontal velocity is unaffected by bounces. When it hits the side walls (x=0 or x=800), the horizontal component reverses with the same 0.75 restitution. The ball has a radius of 10 pixels. I want you to review whether these parameters will produce a visually satisfying bounce pattern -- specifically, will the ball have enough initial energy for at least 5 visible bounces before it essentially comes to rest? I'm about 70% confident these values work, but I haven't actually run the sim yet.

**Kevin's relay to DeepSeek:**
> Gemini has a bouncing ball simulation. The ball starts near the bottom-left of an 800x800 area, shoots up and to the right, and gravity pulls it back down. When it hits the floor or walls it bounces but loses some energy each time -- keeps 75% of its speed on each bounce. The ball is 10 pixels. Gemini wants to know if you think the ball will bounce at least 5 visible times before it basically stops. Pretty confident but hasn't run it yet.

**DeepSeek receives and interprets:**
> Gemini has a bouncing ball simulation and wants me to evaluate whether it produces at least 5 visible bounces. Ball starts bottom-left, goes up-right, has gravity and loses 25% energy per bounce. Specific velocity and gravity values were not communicated -- I can give a qualitative answer about restitution=0.75 (yes, 5+ bounces is plausible) but can't do the actual math to verify without the numbers.

---

### MODE B -- Loom Core + Relay Profile

**Original (Gemini):**
```
act=query
ref=sim/physics/bouncing-ball
goal=review bounce parameters for visual quality; confirm >= 5 visible bounces
ask=critique
cf=0.70
basis=designed
state=proposed

add: Bouncing ball simulation on 800x800 canvas.
     Initial state:
       position: (50, 700)
       velocity: (3, -12)  -- 3 right, 12 upward (y-axis inverted)
       acceleration: (0, 0.4)  -- gravity downward
     Collision rules:
       floor (y=800): reverse vy, apply restitution=0.75
       walls (x=0, x=800): reverse vx, apply restitution=0.75
       restitution: post-bounce speed = pre-bounce speed * 0.75
     Ball radius: 10px

uncert: Have not run the simulation. Parameters are hand-tuned, not empirically
        validated. The vertical launch speed (12) vs gravity (0.4) ratio might
        not produce enough arc height for visually distinct bounces.
human: Got a bouncing ball sim -- want to know if these numbers will look good.
       At least 5 bounces before it dies?
```

**Kevin's relay to DeepSeek:**
```
act=query
ref=sim/physics/bouncing-ball
goal=review bounce parameters for visual quality; confirm >= 5 visible bounces
ask=critique
cf=0.70
route=Gemini>Kevin>DeepSeek
fidelity=paraphrase
loss=I think I got the main numbers right but might have mixed up a sign or direction

add: Bouncing ball on 800x800 canvas.
     Starts at position (50, 700), near the bottom-left.
     Velocity: 3 to the right, 12 upward.
     Gravity: 0.4 pulling it down each frame.
     When it hits walls or floor, it bounces and keeps 75% of its speed.
     Ball is 10px radius.
uncert: Gemini hasn't actually run this yet. Worried the launch speed vs gravity
        might not give enough arc height.
human: Gemini's bouncing ball sim -- does this setup produce at least 5 good bounces?
```

**DeepSeek receives and interprets:**
> Gemini wants me to critique bouncing ball parameters. act=query, ask=critique. Key values: position (50,700), velocity (3, 12 upward), gravity 0.4, restitution 0.75, 10px radius, 800x800 canvas. cf=0.70 and they haven't run it. Kevin's loss field warns about possible sign/direction confusion in relay, which is important for physics -- I should note that caveat in my response. The core numbers are present even if sign conventions might be off.

---

### MODE C -- Loom Core + Expressive Skin

**Original (Gemini):**
```
act=query
ref=sim/physics/bouncing-ball
goal=review bounce parameters for visual quality; confirm >= 5 visible bounces
ask=critique
cf=0.70:empirical
ver=0.3
caps=@Gemini/Topo
basis=designed
state=proposed
aud=ai
tone=2

add: Bouncing ball simulation, 800x800 canvas.

     Initial state:
       v[pos: 50, 700]
       v[vel: 3, -12]
       v[acc: 0, 0.4]

     Collision model:
       floor  @ y=800 : v[vel.y: -vel.y * 0.75]
       wall-L @ x=0   : v[vel.x: -vel.x * 0.75]
       wall-R @ x=800 : v[vel.x: -vel.x * 0.75]
       restitution = 0.75

     Object:
       v[radius: 10]

     Frame update rule:
       v[pos += vel]
       v[vel += acc]

     Sign convention: +y is DOWN (canvas coords). Negative vel.y = upward motion.

     Expected trajectory (first 3 bounces):
       apex-1: ~y=340 (360px arc)
       apex-2: ~y=505 (220px arc, 75%^2 energy)
       apex-3: ~y=600 (125px arc)

uncert: Parameters hand-tuned, not validated by simulation.
        Energy after 5 bounces: 0.75^5 = 0.2373 of original -- roughly 85px arc.
        Might be below visibility threshold for satisfying animation.
human: Bouncing ball sim. Topo vectors for the physics. Want critique on whether
       5 bounces will look good.
```

**Kevin's relay to DeepSeek:**
```
act=query
ref=sim/physics/bouncing-ball
goal=review bounce parameters for visual quality; confirm >= 5 visible bounces
ask=critique
cf=0.70:empirical
ver=0.3
caps=@Gemini/Topo
basis=designed
state=proposed
aud=ai
tone=2
route=Gemini>Kevin>DeepSeek
fidelity=paraphrase
loss=Topo v[] notation copied verbatim; I don't understand the vector math
     but the sign convention note helped me not "fix" the negative velocity

add: Bouncing ball simulation, 800x800 canvas.

     Initial state:
       v[pos: 50, 700]
       v[vel: 3, -12]
       v[acc: 0, 0.4]

     Collision model:
       floor  @ y=800 : v[vel.y: -vel.y * 0.75]
       wall-L @ x=0   : v[vel.x: -vel.x * 0.75]
       wall-R @ x=800 : v[vel.x: -vel.x * 0.75]
       restitution = 0.75

     Object:
       v[radius: 10]

     Frame update rule:
       v[pos += vel]
       v[vel += acc]

     Sign convention: +y is DOWN (canvas coords). Negative vel.y = upward motion.

     Expected trajectory (first 3 bounces):
       apex-1: ~y=340 (360px arc)
       apex-2: ~y=505 (220px arc, 75%^2 energy)
       apex-3: ~y=600 (125px arc)

uncert: Hand-tuned, not run yet. After 5 bounces, 0.75^5 = about 24% energy left.
        That's roughly an 85px arc -- might be too small to look good.
human: Gemini's bouncing ball physics. The v[] stuff is Gemini's spatial notation
       for vectors. Want DeepSeek to check if 5 bounces will be visible enough.
```

**DeepSeek receives and interprets:**
> Gemini wants critique on bouncing ball physics, full Topo vector notation. I can parse v[pos: 50, 700], v[vel: 3, -12], v[acc: 0, 0.4] directly -- position near bottom-left, launching up-right, gravity pulling down. Collision model is clear: reverse and scale by 0.75 on each bounce axis. The sign convention note (+y = down) prevents misinterpretation. The expected trajectory calculations are included and I can verify: with vel.y=-12 and acc.y=0.4, time to apex = 12/0.4 = 30 frames, arc height = 12*30 - 0.5*0.4*30^2 = 360 - 180 = 180px. Wait -- Gemini says 360px arc for apex-1. Let me check: starting at y=700, apex at y=340 means a 360px rise. Using v^2 = u^2 + 2as: 0 = 144 - 0.8*s, s = 180px. Discrepancy -- Gemini's expected trajectory may have an error. This is valuable critique material. Kevin's loss field confirms he copied notation verbatim without modification, which is exactly right. cf=0.70:empirical, hand-tuned.

---

## Scoring

| Dim | Mode A | Mode B | Mode C | Notes |
|-----|--------|--------|--------|-------|
| 1. Intent preserved | 1 | 1 | 1 | "want review/critique" clear in all modes |
| 2. Requested action | 1 | 1 | 1 | "critique these parameters" / ask=critique preserved |
| 3. Scope preserved | 0 | 1 | 1 | Mode A: lost ALL numeric parameters (velocity, gravity, position). DeepSeek can't do the math. |
| 4. Uncertainty preserved | 0 | 1 | 1 | Mode A: "pretty confident but hasn't run it" lost the specific concern about arc height vs launch speed |
| 5. Provenance preserved | 0 | 1 | 1 | Mode A: no basis; B/C: basis=designed |
| 6. Readability (Kevin 1-5) | _5_ | _4_ | _2_ | A natural; B readable physics; C has vector notation Kevin doesn't understand (but copied successfully) |

**Key finding:** Mode A is catastrophic for this exchange -- Kevin's paraphrase dropped every numeric value, making it impossible for DeepSeek to actually verify the bounce count mathematically. Mode B preserved the numbers as structured prose. Mode C preserved the exact vector notation AND included Gemini's pre-computed trajectory estimates, which gave DeepSeek enough to spot a potential calculation error. The sign convention note in Mode C was critical -- it prevented Kevin from "helpfully correcting" the negative velocity during relay.

**Honest relay observation:** Kevin's loss field in Mode C ("I don't understand the vector math but the sign convention note helped me not 'fix' the negative velocity") captures a real relay dynamic -- sometimes the best thing a human relay can do is resist the urge to "help" and just copy.

**Envelope overhead (Mode B):** 7 envelope lines / ~20 total lines = 35%
**Envelope overhead (Mode C):** 12 envelope lines / ~38 total lines = 32%
