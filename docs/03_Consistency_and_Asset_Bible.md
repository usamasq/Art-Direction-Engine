# Modular AI Visual System — 03 · Consistency & Asset Bible

*How to keep a specific product or character identical across many outputs — a static series, or a multi-shot video. This module holds the locked assets; the Statics module (04) and Video module (05) both pull from it. Engine-specific mechanics (how a given model accepts references) live in Doc 06.*

---

## 1. The two kinds of consistency (don't confuse them)

- **Asset consistency** (this document): the *thing* stays identical — the bottle's label, the mascot's face, the jersey's number — across every frame.
- **World consistency** (Doc 05): the *scene* stays identical — the room, the light direction, the time of day — across camera angles.

They fail independently. An engine can render your exact bottle inside a room whose window jumped walls between shots. This document fixes the first; the Video module fixes the second. Use both together for video.

---

## 2. The Asset Bible entry

One entry per recurring product or character. Fill it once; reuse it everywhere. This entry is the single source of truth for that asset — no module re-describes it.

```
ASSET ENTRY
- ID / name:            ____
- Type:                 product / character / set-piece
- Canonical description: ____  (the locked verbal description, used verbatim
                          in prompts so wording never drifts)
- Real-world dimensions: ____  (feeds the scale system, Doc 02 §4)
- Reference sheet:      ____  (file/URL of the multi-angle sheet — see §3)
- Material / finish:    ____  (from Profile F5, pinned for this asset)
- Do-not-vary list:     ____  (the features that MUST stay constant:
                          label text position, logo, colourway, proportions,
                          a character's hair/eyes/wardrobe)
- May-vary list:        ____  (what's allowed to change: angle, lighting on it,
                          condensation, expression for a character)
- Style-lock handle:    ____  (seed / sref / reference-set ID, from Doc 06)
```

The **canonical description** is reused word-for-word across prompts. Re-paraphrasing it each time is how labels morph and faces change. Lock the words.

---

## 3a. Building your references — *runnable, before anything else*

References are images you must **make**, so they get **runnable prompts too** — not just a phrase like "a sunlit kitchen." This is the same "described vs runnable" rule applied at the foundation: if the references aren't real images, nothing downstream is consistent. There are three builders. Pull every look detail (light, palette, materials, setting) from the active Art Direction Profile (Doc 01).

### A. Scene / environment reference (the empty set)
Generate the location with **no product in it yet** — a clean plate the master frame will place the asset into. Build the prompt from the Profile's lighting (F4), palette (F3), materials (F5), and setting vocabulary (F6).
```
PROMPT → paste into Nano Banana Pro:
[Profile setting from F6], [Profile lighting F4 — source, direction, time], [Profile
materials/textures F5], [Profile palette F3]. Empty of any product. [Composition/lens].
A defocused [Profile negative-space fill F9] area at [position] for later copy. No text,
no people unless specified. --ar [aspect]
```

### B. Product → multi-angle reference sheet (the most important builder)
You almost always start with **one product photo**, not a sheet. Convert it into a clean multi-angle sheet *once*; that sheet then locks the product across every future still and video. Two cases:

**B1 — you have a clean packshot** (product on white/simple background):
```
PROMPT → paste into Nano Banana Pro  (attach: the single product photo):
Using the attached product photo as the exact reference: produce a clean multi-angle
reference sheet of THIS product on a plain neutral grey background — front, 3/4, side,
back, and a close detail crop of the label/logo. Keep the label text, typography,
colours, proportions and shape IDENTICAL to the photo in every view. Even soft studio
light, no scene, no props, no added text. --ar 1:1
```

**B2 — your only photo is in a setting** (on a shelf, in a hand, busy background) — isolate first, then rotate:
```
STEP 1 — isolate:
PROMPT → paste into Nano Banana Pro  (attach: the in-setting photo):
Extract ONLY the [product] from the attached photo and place it alone on a plain neutral
grey background, lit evenly. Keep the label, colours and shape exactly as in the photo.
Remove all background, hands, and props. --ar 1:1
STEP 2 — rotate into a sheet:
PROMPT → paste into Nano Banana Pro  (attach: the isolated image from Step 1):
Using this isolated product: produce a multi-angle reference sheet — front, 3/4, side,
back, and a label detail crop — on the same neutral background, label and proportions
identical across all views. --ar 1:1
```
▸ **Approve the sheet, then add the product's real dimensions to its Asset Bible entry (§2).** This sheet is now the product's permanent reference — reuse it everywhere.

### C. Character → turnaround sheet (when there's a recurring person)
```
PROMPT → paste into Nano Banana Pro  (attach: the character photo if you have one):
[A turnaround/character sheet of [person, wardrobe from Profile F6]] on a plain neutral
background: front, 3/4, and profile views, plus an expression row (neutral, smiling,
mid-action) and one full-body shot for proportions. Keep face, hair, build and wardrobe
identical across every view. Even light, no scene. --ar 1:1
```

**Three rules that decide whether references actually work** (apply to every builder and every downstream use):
- **Label each reference's role in the prompt.** The biggest single lever — "image 1 = product, preserve label/shape/colour; image 2 = scene." Unlabelled references make the model guess what to keep, and it guesses wrong.
- **Cap at ~6 images; front-load the critical 2–3.** More is *worse* — past ~6 references accuracy *degrades*. Must-hold elements first.
- **Lean on session memory (Nano Banana Pro).** Define the asset fully in the first prompt of a session; later prompts in the same session need only the new angle/action.

---

## 3. Reference sheets — what they are

The most reliable way to keep an asset identical is to feed the engine **dedicated reference images** (built via §3a), not just text. Modern image models (Nano Banana Pro, Flux, Midjourney V7) fuse a reference into new scenes far better than they follow a written description.

**For a product:** a clean **multi-angle sheet** — front, 3/4, side, back, plus a detail crop of the label/logo — on a neutral background. Reconstructs the object from any new angle while keeping packaging exact.

**For a character:** a **turnaround** — front, 3/4, profile — plus an expression row and a full-body shot. Holds a face and outfit steady across shots.

---

## 4. The master-frame method

The core trick for consistency, used in both statics series and video:

```
1. Generate ONE hero frame and get it perfect — composition, asset, light, palette.
   This is the MASTER.
2. Generate every other frame (other angles, other scenes, other beats) by feeding
   the MASTER back in as a reference image, changing only what must change
   ("same scene and light, camera now low and behind"; "same bottle, now on a
   courtyard table").
3. Never re-roll a related frame from text alone — derive it from the master.
```

Deriving from an image instead of from words is what keeps the *world* and the *asset* stitched together. It is cheaper, faster, and far more consistent than independent text generations.

---

## 5. Seed & style locking

Beyond reference images, lock the engine's own consistency handles (specifics in Doc 06):
- **Seed** — reusing a seed keeps an engine's "interpretation" stable across small prompt changes.
- **Style reference** (`--sref` in Midjourney, reference-set in others) — locks the overall look across a campaign.
- **Omni / character reference** (`--oref` in Midjourney V7, image refs elsewhere) — locks the specific asset.

Record each asset's chosen handle in its entry (§2) and reuse it for the whole campaign. Store them in the Profile's style-lock table (01, F12) too, so feed cohesion and asset cohesion share one record.

---

## 6. How scale ties in

The asset's **real-world dimensions** (§2) feed directly into the Core Grammar's scale system (Doc 02 §4). Because the dimension is recorded once here and referenced everywhere, the bottle is the same physical size relative to the hand in the macro shot and in the wide shot — no per-prompt guessing. This is the link that stops scale drift across a series.

---

## 7. Consistency quick-procedure

```
Before generating a series or a video with a recurring asset:
1. Create / locate the Asset Bible entry (§2).
2. Make the reference sheet if it doesn't exist (§3).
3. Generate the master frame and approve it (§4).
4. Derive all further frames from the master + the reference sheet (§4).
5. Reuse the same seed / sref / oref handle throughout (§5).
6. Check each output against the asset's do-not-vary list (§2).
```

---

*Doc 03 of 7. Holds locked assets. Used by 04 and 05; mechanics deferred to 06.*
