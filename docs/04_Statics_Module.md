# Art Direction Engine — 04 · Statics Module

*For still images: one static, or a series of statics that share the same product/asset. Pulls build rules from the Core Grammar (02) and asset-locking from the Asset Bible (03). Brand look comes from the active Profile (01).*

---

## 1. Single static

The simplest path. One image, one moment.

```
1. Confirm the active Profile (01) and the Mode (Profile F7) for this content.
2. If a recurring asset appears, load its Asset Bible entry (03).
3. Assemble the prompt with the Core Grammar (02): one choice per layer,
   negative space as an in-palette defocused region (02 §3), scale anchored (02 §4).
4. Append the negative block; set the aspect (02 §5).
5. Translate to the chosen engine (06).
6. Return 2–3 framing variants (Operating Contract §4.3).
```

**Output template (neutral, pre-engine):**
```
[L1 render + lens + DoF]
[L2 light from Profile F4 / Mode]
[L3 subject from F6 or locked asset from 03 + action + texture + real dimension]
[L4 environment from F6 + palette context F3]
[L5 composition F8 + negative-space region F9 (defocused, in-palette) + in-frame proportion]
[negative block]
[aspect]
```

---

## 2. Static series — same asset, many scenes

A set of posts using the **same product** across different scenes/days (a six-post product run, a weekly slot). The whole point is that the product is unmistakably identical while the scenes vary. This is where most series quietly break — the product subtly changes between posts.

### The series procedure
```
1. Lock the asset first (Asset Bible 03 §7): entry, reference sheet, master frame.
   Build the sheet tight — label each reference's role and cap at ~6 images, front-
   loading the critical 2–3; more degrades accuracy (03 §3).
2. Establish a SERIES MASTER — one approved hero image of the asset in-world,
   in the chosen Mode. This sets the look the whole series inherits.
3. For each new post, DERIVE from the master (03 §4): feed the master + the asset
   reference sheet back in (labelling each: "image 1 = product, preserve label/shape
   /colour; image 2 = master"), and change only the scene/action per the Profile's
   vocabulary (new setting from F6, new cast, new light angle within F4). Run the
   whole series in ONE Nano Banana Pro session so its memory holds the locked asset
   (03 §3); later posts then need only the new scene.
4. Keep these LOCKED across the series:
   - the asset itself (do-not-vary list, 03 §2)
   - the seed / sref / oref handle (03 §5; Profile F12)
   - the lens family (02 §4.3) — so the product reads the same physical size each time
   - the Mode and palette (Profile F3, F7)
5. Let these VARY for freshness:
   - setting, cast, action, time-of-day within the light signature,
     negative-space placement per layout.
```

### What keeps a series coherent
| Locked (never changes) | Varies (keeps it fresh) |
|---|---|
| The product (label, colourway, proportions) | Setting / environment |
| Seed / style-ref handle | Cast / people |
| Lens family + scale anchor | Action / interaction |
| Mode + palette | Light angle (within the signature) |
| Negative-space *treatment* | Negative-space *placement* per aspect |

### Series output
Return the **series master prompt** first, then a short **derive instruction** per subsequent post (not a full fresh prompt each time):
```
SERIES MASTER: [full assembled prompt for the hero image]
POST 2 (derive): same master + asset sheet; change setting to [F6 option],
   cast to [F6 option], keep asset/seed/lens/Mode locked.
POST 3 (derive): ...
```

---

## 3. Common drift to catch (statics)
- Negative space rendering as a white box → re-derive from the in-palette menu (02 §3).
- Product size jumping between posts → confirm the lens family and scale anchor are locked (02 §4; 03 §6).
- Label/logo morphing across the series → you re-paraphrased the canonical description; paste it verbatim and lean on the reference sheet (03 §2–3).
- Series looking like unrelated images → you generated each from text instead of deriving from the master (03 §4).

---

*Doc 04 of the Art Direction Engine. Statics. Uses 02 + 03; translated by 06.*
