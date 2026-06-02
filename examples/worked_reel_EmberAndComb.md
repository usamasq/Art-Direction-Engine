# Worked Example — Ember & Comb "The Drizzle" Reel (runnable format)

*A complete, non-technical-operator-runnable video deliverable, built from the [Ember & Comb Profile](profile_EmberAndComb.md) in **Drizzle** mode. It is the gold standard for what an output of this system should look like: read the header, follow the numbered Steps, copy only the marked prompt blocks. Demonstrates the stills-first loop ([Doc 05 §5](../docs/05_Video_Scene_Module.md)), the runnable-deliverable format ([Doc 00 §4.1a](../docs/00_System_Operating_Contract.md)), and the pre-flight gate ([Doc 00 §4.8](../docs/00_System_Operating_Contract.md)). Everything is invented — no real brand.*

Brand Profile: Ember & Comb · Mode: Drizzle · Output: 9:16 reel (~10s).

---

```
HOW TO RUN THIS  (read first)
You'll make still images in Nano Banana Pro, then animate them in Gemini Omni.
Each STEP is one action, in order. "PROMPT →" blocks are text to copy exactly.
The Scene Sheet and Ledger are context to read, not paste.
The copy list + checks at the end are for your editor, after all clips exist.
```

## SCENE SHEET  *(reference — read once, don't paste)*
- **Space:** a dark rustic kitchen at dusk; a worn oak board on a communal table, crispy fried chicken plated on it, the Ember & Comb honey jar + wooden dipper beside it. Fixed geometry: hearth/warm light always **camera-left**; jar sits front-right of the board.
- **Light & time:** single low warm hearth light from **camera-left**, soft-edged shadows, faint smoky haze, dusk. LOCKED.
- **Palette & grade:** Charcoal `#2A2422` canvas; Amber-honey `#C8841E` on the pour; Ember-red `#9E3B22` chili cue; deep warm glow, rich-not-neon.
- **Assets (fixed positions):** Ember & Comb honey jar + dipper — front-right of the board; the fried chicken — centre, on the worn oak board.
- **Lens family:** 50mm coverage + 100mm macro for the insert.
- **Negative-space:** upper area (Shot 1) / lower-third (Shot 4) — a defocused charcoal plaster wall in Warm Ash, never white.
- **Style-lock handle:** `master_frame_ember_v1` + fixed seed.
- **Lock vs evolve:** kitchen + light LOCKED; the honey on the food EVOLVES via the ledger (none → drizzling → pooled).

## STATE LEDGER  *(reference — read once, don't paste)*
- Beat 1: jar closed, food bare. → Beat 2: dipper lifted, first amber ribbon falling. → Beat 3 (macro): ribbon lands, chili flecks, honey starts to pool. → Beat 4: honey glistening and pooled, a hand tears a piece away.

---

## STEP 1 · Make your reference images (Nano Banana Pro)

Make and approve these **first** — everything downstream attaches them. Work in one session; label each reference's role; cap at ~6 images. These are prompts to paste, not descriptions.

**1a. Scene/environment reference** (the empty set, built from the Profile):
```
PROMPT → paste into Nano Banana Pro:
A dark rustic kitchen at dusk — worn oak table, seasoned cast iron, coarse linen, a
charcoal plaster wall behind. Single low warm hearth light from camera-left, soft-edged
shadows, faint smoky haze, deep amber glow against charcoal. Empty worn oak board on the
table, no product yet. 50mm, shallow depth on the kitchen behind. Charcoal-and-amber
palette, matte surfaces. No text, no people. --ar 9:16
```

**1b. Product sheet — convert the single jar photo into a multi-angle sheet** (you start with one packshot):
```
PROMPT → paste into Nano Banana Pro  (attach: the one Ember & Comb jar photo):
Using the attached product photo as the exact reference: produce a clean multi-angle
reference sheet of THIS honey jar on a plain neutral grey background — front, 3/4, side,
and a close detail crop of the label. Keep the label text, typography, colours, the amber
honey colour, proportions and shape identical to the photo in every view. Even soft light,
no scene, no props, no added text. --ar 1:1
```
*If your only jar photo is in a busy setting, first paste an isolate prompt — "extract only the honey jar onto a plain grey background, label and amber colour exact" — then run the sheet prompt on that.*

**1c. Record real dimensions** in the Asset Bible after approving the sheet: jar ~8 cm tall · wooden dipper ~16 cm. (These lock the pour proportions across shots.)

---

## STEP 2 · Make the master frame (Nano Banana Pro)

Work in **one session** so its memory holds the locked jar as you derive later shots. Turn on "thinking" mode.

> **PROMPT → paste into Nano Banana Pro**  *(attach: scene ref + jar sheet)*
> image 1 = scene/layout reference (preserve the kitchen geometry + camera-left hearth light); image 2 = the Ember & Comb jar sheet (preserve label, shape, amber colour). A dark rustic kitchen at dusk, single low warm hearth light from camera-left. On a worn oak board: crispy golden fried chicken centre, the Ember & Comb honey jar with its wooden dipper resting front-right, lid off. Deep amber glow against charcoal, faint smoky haze, matte wood and iron, shallow depth on the dark kitchen behind. 50mm, low and close, asymmetric. Upper-left kept as a soft defocused charcoal plaster wall in warm ash for copy (not white). No deformed hands, no plastic sheen, honey-glossy only. `--ar 9:16`

▸ **Approve this image before continuing.** Save it as `master_frame_ember_v1`.

---

## STEP 3 · Make each shot's still(s) (Nano Banana Pro)

Paste these in order. Where a shot reuses the previous frame, no new prompt is needed.

### Shot 1 — establish the board  *(single still)*
Reuse the approved `master_frame_ember_v1` — **no new prompt.**

### Shot 2 — the dipper lifts, first drizzle  *(two-state: start + end)*
- **Start still:** reuse `master_frame_ember_v1` — no new prompt.
> **END PROMPT → paste into Nano Banana Pro**  *(attach: master frame + jar sheet)*
> Using the attached master frame and jar reference: same dark kitchen, hearth light stays camera-left, board and chicken unchanged in place — but a cook's hand now lifts the wooden dipper up out of the jar and a first thick glossy ribbon of amber chili honey is falling from it toward the chicken, a few ember-red chili flecks suspended in the amber. Keep the label and amber colour exact, honey thick and slow. 50mm, deep warm glow, upper-left kept as a defocused charcoal wall reserved for copy (not white). `--ar 9:16`

### Shot 3 — the drizzle lands · **macro insert**  *(two-state: start + end)*
*New angle (100mm macro), so the start frame is written fresh — it can't be the wide pivoted.*
> **START PROMPT → paste into Nano Banana Pro**  *(attach: Shot 2 end still + jar sheet)*
> Using the attached frame and the jar reference: re-frame to a tight 100mm macro on the chicken — same hearth light from camera-left, same charcoal-and-amber palette and grade as the wider shots — a thick glossy ribbon of amber chili honey mid-air just above the crispy crust, ember-red chili flecks suspended in it, the dark kitchen fully out of focus behind. Honey thick and glossy. `--ar 9:16` *(macro insert — no copy overlay, so no reserved negative space here.)*

> **END PROMPT → paste into Nano Banana Pro**  *(attach: the start still just above)*
> Same macro frame, but the honey has landed — a glossy amber pool spreading over the crispy crust, slow drips down the side, chili flecks settling in the pool. Everything else identical. `--ar 9:16`

### Shot 4 — someone reaches in  *(two-state: start + end)*
*Re-establishes 50mm after the macro and brings in the human, so the start frame is written fresh.*
> **START PROMPT → paste into Nano Banana Pro**  *(attach: Shot 2 end still + jar sheet)*
> Using the attached frame and the jar reference: 50mm, pull back to show the board with the honey-glazed chicken glistening, the jar front-right, hearth light still camera-left, kitchen geometry unchanged — a person (warm, candid, partly in frame) sits at the worn table leaning in. Honey pooled and glossy on the chicken. Lower-third kept as a defocused charcoal wall in warm ash reserved for the closing copy (not white). `--ar 9:16`

> **END PROMPT → paste into Nano Banana Pro**  *(attach: the start still just above)*
> Same frame, but the person's hand has reached in and torn a glazed piece away, a thread of glossy honey stretching from it. Everything else identical. `--ar 9:16`

---

## STEP 4 · Animate each still (Gemini Omni)

Paste each brief into Gemini Omni and attach the listed still(s). These describe **motion only** — the product and set are already locked in the stills.

### Shot 1
> **PROMPT → paste into Gemini Omni**  *(attach: Shot 1 still)*
> Goal: animate the attached still into a ~2.5s opening shot. Input role: the still is the product+scene reference — preserve it exactly, animate only the motion. Motion: faint smoke drifts through the hearth light, the amber glow flickers gently; everything else holds still. Constraints: keep label and amber colour exact; no engine text. Audio: a low hearth crackle, quiet room tone.

### Shot 2  *(first-and-last-frame)*
> **PROMPT → paste into Gemini Omni**  *(attach: Shot 2 start still + end still)*
> Goal: interpolate between the two attached frames over ~2.5s. Input role: start = frame 0, end = final frame; animate only the motion between them. Motion: the hand lifts the dipper from the jar and a thick glossy ribbon of honey begins to fall toward the chicken; the rest of the board stays still. Constraints: honey thick and slow with realistic weight, label un-warped. Audio: a soft viscous lift-and-stretch of honey.

### Shot 3  *(first-and-last-frame, macro)*
> **PROMPT → paste into Gemini Omni**  *(attach: Shot 3 start still + end still)*
> Goal: interpolate between the two attached macro frames over ~2.5s. Motion: the honey ribbon lands and spreads into a glossy pool over the crispy crust, chili flecks settling; shallow macro depth. Constraints: realistic viscous flow, crisp crust texture, honey glossy. Audio: a faint sizzle as honey meets warm food.

### Shot 4  *(first-and-last-frame)*
> **PROMPT → paste into Gemini Omni**  *(attach: Shot 4 start still + end still)*
> Goal: interpolate between the two attached frames over ~2.5s. Motion: the person's hand reaches in and tears a glazed piece away, a thread of honey stretching and breaking. Constraints: honey thread realistic, label exact, warm candid feel. Audio: a crisp tear, a soft satisfied breath, hearth crackle underneath.

---

## STEP 5 · Hand to your editor

*AFTER all clips are generated — for your editor, not for the engines. Total ≈10s across the four clips; copy is placed only on the shots that reserve negative space (Shots 1 and 4 — not the Shot 3 macro).*

**Copy / compositing plan** *(set type in post — never engine-rendered; one clip per line):*
- **Shot 1 (open)** — region: upper-left — line: "Honey with a bite." — notes: warm-toned type, brand-warm open.
- **Shots 2–3** — no copy; let the pour and the macro breathe (optional small brand mark only).
- **Shot 4 (close)** — region: lower-third — line: "Ember & Comb — on everything." — notes: composite the logo here.

**Render-QC watch list** *(check in the rendered clips):*
- **Honey reading thin/runny** instead of thick and glossy → if it looks watery, re-derive that still emphasising "thick, slow, viscous"; don't re-roll from text.
- **Light flipping to camera-right** in any clip → reject; the hearth light is locked camera-left.
- **The chili cue vanishing** (reads as plain honey) → ensure the ember-red flecks survive the animation; flag if they wash out.
- **Label drift** on the jar between the 50mm and 100mm shots → re-derive from the jar sheet, not from text.

---

## Why this layout is the standard
- **A stranger can run it.** The header names the two tools and how to read the doc; every prompt block names its tool and attachments; the Scene Sheet/ledger are tagged "don't paste"; post-production is walled off at the end. (Doc 00 §4.1a.)
- **Numbered Steps are the spine** — make refs → master → stills → animate → hand off — so there's never ambiguity about what to do next or what to copy.
- **Each still is a runnable prompt, not a description**, and two-state moments (the lift, the macro landing, the reach-in) write both frames; reused frames just cite the handle.
- **Continuity is enforced by the stills:** where the angle holds, a shot's start frame is the previous shot's end frame; where the angle changes (Shots 3–4), the start frame is written fresh but carries the correct honey state from the ledger.
- **Copy is mapped only onto frames that reserve space** (not the Shot 3 macro), and the budget fits 10s.
- **An emotional/lifestyle brief keeps its human** — Shot 4 brings a person in to share the food, rather than staying product-only (Doc 00 §4.8.5).

*Reference example. Reuse this exact layout for any multi-beat product reel.*
