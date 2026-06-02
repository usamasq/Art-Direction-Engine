# Art Direction Engine — 05 · Video / Scene Module

*For video: multi-shot scenes with several camera angles and elements that must read as one continuous filmed space, and sequences where things progress over time. Pulls build rules from the Core Grammar (02) and asset-locking from the Asset Bible (03). The brand look comes from the active Profile (01); engine syntax from Doc 06.*

---

## 1. The module's one job: continuity

Make many separate generations read as **one continuous scene**. The module does **not** re-describe the product or character each shot — that is the Asset Bible's job (03). Two different problems, handled in two places:

- **Asset consistency** → Asset Bible (03): the *thing* stays identical.
- **World consistency** → this module: the *scene* stays identical — room, light, time, spatial layout — across every angle.

Both are needed for video. An engine can render your exact bottle in a room whose window jumped walls between cuts.

---

## 2. The Scene Sheet — the single source of truth for the world

Written **once** per scene, then inherited by every shot. It holds the constants. The principle: **describe the world once; afterwards describe only what changes.**

```
SCENE SHEET
- Scene name:        ____
- Space:             ____  (location + fixed architecture; where walls/windows/
                      furniture sit — the geometry that must agree across angles)
- Light & time:      ____  (single source, direction, colour temp, time of day —
                      LOCKED; shifting light is the #1 tell that shots don't match)
- Palette & grade:   ____  (from Profile F3)
- Assets present:    ____  (which Asset Bible entries appear, and WHERE they sit
                      in the space — the blocking)
- Lens family:       ____  (the scene's optical character — from Profile F8 /
                      Grammar 02 §4.3. ONE focal length if possible. If inserts need a
                      different one, declare the WHOLE family up front, e.g. "35mm
                      coverage + 60mm macro inserts" — never let a shot silently switch
                      to "macro" when the sheet said 35mm; that breaks scale and look)
- Negative-space:    ____  (the defocused in-palette region for copy, Grammar 02 §3 —
                      declared once so it isn't reinvented as a white box per shot)
- Style-lock handle: ____  (MUST point to the actual master frame / seed / reference-set
                      ID — 03 §5. "Reused across beats" is not a handle; name the thing)
- Mode:              ____  (active Profile Mode, F7)
- Lock vs evolve:    ____  (see §6)
```

Everything below the Scene Sheet is a **delta** on it.

---

## 3. Shots as deltas + continuity anchors

Each shot is a short statement of only what changes, plus the anchors that stitch the cut.

```
SHOT n
- Camera:    ____  (position, angle, lens within the family, movement)
- Action:    ____  (what changes in this beat — the only new content)
- Anchors:   ____  (2–3 fixed cues that MUST reappear so the eye stitches the cut:
              "window stays camera-left", "cup stays half-full", "jacket open")
```

**Continuity anchors are the actual mechanism** that makes angle B feel like the same room as angle A. Without them the engine quietly re-decides the layout. Always name them — and **restate them inside the still prompt itself** (e.g. "window light stays camera-left, shelf grid unchanged"), not only in the shot header. A re-framed or angle-change still makes the image engine recompose, and naming the locked constants in the prompt stops it silently re-deciding geometry. This matters most on shots that change angle or lens.

---

## 4. The two video jobs

Most reels blend these; each shot declares which it is.

### 4.1 Multi-angle coverage of one moment
The same moment from wide, medium, over-the-shoulder, macro insert. Continuity here is **spatial** — the geometry must agree. If light came from the left in the wide, it can't come from the right in the close-up.

Standard coverage set:
```
- WIDE: establish the space + blocking
- MEDIUM: the subject + the asset
- OTS / reverse: relationship / point of view
- MACRO INSERT: the hero detail (label, hands, the pour)
```
Rule: **all angles resolve to the same Scene Sheet geometry**, and **each angle is its own still** — a video model can't be trusted to pivot to a new angle and keep the product/world right, because that angle isn't in the reference frame. So coverage from four angles = **four derived stills**, each made from the master frame (03 §4), not one still and not fresh text. Each still is then animated motion-only (§5).

### 4.2 Sequential beats over time
A 10–15s arc where things progress (exhausted → pours drink → relief; or a build-up reel). Continuity here is **temporal** — state carries forward. If the glass was full in beat 2, it isn't full again in beat 4.

Track a tiny **state ledger**:
```
STATE LEDGER
- beat 1: bottle sealed, cup empty
- beat 2: bottle tilting, pour begins
- beat 3: cup half-full
- beat 4: subject drinks, cup lower
```
Each shot must respect the ledger so progression stays logical.

---

## 5. The production loop *(stills-first — the canonical workflow)*

This is the reliable path: **lock the look as stills, then animate.** A video model only keeps the product/world consistent for **what's already in the still it's handed** — it animates a frame, it doesn't invent a faithful product from text. So the atomic unit is **one still → its animation, motion-only**, repeated per shot.

```
STEP 1 — Prompt series
  Write the Scene Sheet (§2) and the shot list (§3) from the Profile + Grammar.

STEP 2 — Scene & asset references (BEFORE hero frames)
  Generate the environment / layout reference for the space, AND a multi-angle
  reference sheet for each recurring product/character (03 §3). These anchor
  everything downstream. (This step is what most workflows skip.)

STEP 3 — Master frame -> a derived still PER ANGLE (image model: Nano Banana Pro)
  Generate ONE master hero frame. Then derive a SEPARATE still for every distinct
  framing/angle, each from the master + the asset sheets, changing only camera/action
  (03 §4). A video model can't be trusted to swing to a new angle and keep the product
  /world right — the new angle isn't in the reference frame. So multi-angle coverage =
  N stills, one per angle, not one still for the scene. (Share a still between two shots
  only if the frame is identical and just the motion differs.)
  - Do all of a scene's derivations in ONE Nano Banana Pro session: define the asset
    fully in the first prompt, then later stills need only the new angle/action —
    session memory recalls the locked asset (03 §3). Label each reference's role and
    keep total references ~6 or fewer (03 §3).

STEP 4 — Stills -> video (video model: Gemini Omni), MOTION-ONLY
  Animate each approved still with a prompt that describes ONLY how it moves — never
  re-describe the product, set, or light (already locked in the still's pixels). Label
  the still's role ("this is the product+scene reference — preserve it; animate the
  motion below"). Use Omni's 5-part brief: Goal / Input role / Scene / Motion / Constraints.
  - Default: one still, describe its motion (incl. SMALL camera moves — slight push-in,
    gentle pull-back).
  - Two-state -> FIRST-AND-LAST-FRAME (start still + end still, interpolate). TWO causes:
      a) subject motion arc — hand grabs product, pour, door; and
      b) a LARGE camera move — orbit, big push-in, jib, whip — because the far side of
         the subject / the geometry the camera moves toward isn't in the start frame, so
         one still can't drive it. Supply a start-angle still and an end-angle still.
  Route to the engine whose feature fits (06):
     - default: native audio + multi-shot continuity + first/last-frame -> Gemini Omni
     - explicit camera/motion-brush control -> Runway Gen-4.5
     - standalone single-shot, max fidelity, no continuity needed -> Seedance 2.0
```

Why this order wins: by Step 4 the hard parts (composition, asset, light, layout) are already frozen into images, so the video model only solves motion. You can art-direct a frame you can see; you can't art-direct one you never generated.

**Copy mode for video (Grammar 02 §3a).** Two ways copy lands on a reel:
- **Reserve (default):** every copy-bearing still reserves in-palette negative space (§3); your editor composites the type in the real brand font in Step 5. Required for brand-exact fonts, logos, legal lines, and non-Latin/Arabic.
- **Render:** the headline is baked into the **still(s)** it appears on during Step 3, using a text-capable image engine (Doc 06) and the brand type spec (Profile F13). **Never ask the video model to generate live type** — it mangles text; put it in the still, then animate motion-only. Moving/kinetic type is an editor (post) task, not a generation task.

---

## 6. Locked vs evolving toggle

Declared in the Scene Sheet. Serves both product work and narrative arcs.
- **Locked:** maximum consistency, minimal variety — the world holds perfectly still. Best for product and matchday work.
- **Evolving (declared drift):** a controlled change across the scene — "golden hour deepening across the reel", "neon intensity rising to the final beat." The *change itself* is part of the Scene Sheet so it's intentional, not accidental drift.

---

## 7. Video output template

The loop (§5) **is** the structure of the deliverable — not an afterthought in notes. Each shot carries its Step-3 still and its Step-4 animation explicitly.

The deliverable must be **runnable top-to-bottom by a non-technical operator** (Doc 00 §4.1a). Use this shape — a "how to run this" header, the Scene Sheet tagged as reference, then a numbered Step sequence where every paste-able prompt is marked with its model and attachments, and post-production sits at the end.

```
HOW TO RUN THIS  (read first)
You'll make still images in Nano Banana Pro, then animate them in Gemini Omni.
Each STEP is one action, in order. "PROMPT →" blocks are text to copy exactly.
The Scene Sheet and Ledger are context to read, not paste.
The copy list + checks at the end are for your editor, after all clips exist.
```

**SCENE SHEET** *(reference — read once, don't paste)* — [filled per §2; lens family + style-lock handle concrete]
**STATE LEDGER** *(reference — read once, don't paste)* — [beat-by-beat state, if sequential]

**STEP 1 · Make your reference images (Nano Banana Pro)** — paste the actual builder prompts from Doc 03 §3a (not phrases):
- *Scene/environment reference* — a runnable prompt built from the Profile (light F4, palette F3, materials F5, setting F6), empty of product.
- *Product → multi-angle sheet* — the runnable conversion prompt (clean packshot = one prompt; in-setting photo = isolate first, then rotate). Add real dimensions to the Asset Bible after approving.
- *Character turnaround* — if a recurring person appears.

**STEP 2 · Make the master frame (Nano Banana Pro)**
```
PROMPT → paste into Nano Banana Pro  (attach: scene ref + asset sheets):
[the one hero still prompt that sets the world]
```
Approve before continuing; save as the style-lock handle.

**STEP 3 · Make each shot's still(s) (Nano Banana Pro)** — in order; reused frames just cite the handle:
```
Shot 1 (single still): reuse master  — OR —
  PROMPT → paste into Nano Banana Pro (attach: [refs]): [runnable still prompt]
Shot 2 (two-state):
  START → reuse prior end still — OR — PROMPT → paste into Nano Banana Pro (attach: [refs]): [start prompt]
  END   → PROMPT → paste into Nano Banana Pro (attach: start still + [refs]): [end prompt]
```

**STEP 4 · Animate each still (Gemini Omni)** — motion-only; attach the listed still(s):
```
Shot n → PROMPT → paste into Gemini Omni (attach: [still / start+end stills]):
[Goal / Input role / Scene / Motion / Constraints / Audio]
```

**STEP 5 · Hand to your editor** — *AFTER all clips are generated.* Present the copy plan as a **list, not a table** — one clip per line:
```
Shot 1 — region: [where] — EN: "[line]" — AR: "[line]" — notes: [logo? none?]
Shot 2 — ...
```
Plus a Render-QC watch-list: 2–3 specific things to check in the rendered clips.

**Four rules behind the format:**
- **Runnable by a stranger.** A first-time reader must be able to tell what to copy first and where (Doc 00 §4.1a). The three text kinds (paste-prompt / reference / post-production) are visually distinct and labelled, and each prompt names its model + attachments.
- **Every still is a runnable prompt, not a description.** If a shot needs a new frame (and every two-state shot needs both a start and an end frame), write the actual image-engine prompt with references named. A described-but-unwritten still never gets generated, and the video step then has nothing to animate.
- **One still per angle.** Every distinct framing/angle gets its own derived still (§4.1, §5). Don't expect one still to cover multiple angles.
- **Animation is motion-only.** The Step-4 prompt describes movement and timing only — product, set, and light are locked in the still. Use **first-and-last-frame** (start → end) for **both** a two-state subject motion (grab, pour, door) **and** a large camera move (orbit, big push-in, jib, whip); small moves animate fine from one still. Never hand a two-state beat to the engine as text-only.

---

## 8. Common drift to catch (video)
- Room layout changes between angles → anchors not named (§3); derive from master (§5 step 3).
- Light direction flips between shots → Scene Sheet light not locked (§2).
- Asset morphs across shots → use the reference sheet + verbatim canonical description (03).
- Scale of the subject jumps → lens family not held constant (02 §4.3; §2 lens family).
- Progression makes no sense (full glass reappears) → no state ledger (§4.2).
- Tried to text-to-video the whole thing → return to stills-first (§5).
- **Copy scheduled over a full-bleed macro** → the timing map puts a tagline on a shot with no negative space. Confine copy to shots that reserve space, or reserve a lower-third in the macro too (Doc 00 §4.8.1).
- **A "treat yourself / family / ritual" brief rendered as product-only** → an emotional brief lost its human. Add a person or surface the choice (Doc 00 §4.8.5).
- **Continuity skips a beat** → a shot's start frame isn't the previous shot's end frame and a state change (or a hand entering/leaving) happens off-screen. Derive the start from the prior end where the angle holds; if the angle changes, write the new start frame carrying the correct state (incl. whether a hand is present).
- **Citation tags / broken fences in the prompt text** → retrieval artifacts pasted into the deliverable. Strip them; every prompt is clean paste-ready text (Doc 00 §4.8.6).

---

*Doc 05 of the Art Direction Engine. Video. Uses 02 + 03; translated by 06.*
