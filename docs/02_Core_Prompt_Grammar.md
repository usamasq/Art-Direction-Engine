# Art Direction Engine — 02 · Core Prompt Grammar

*Brand-neutral mechanics. How any prompt is built, regardless of brand. The brand values come from the Art Direction Profile (01); the asset facts come from the Asset Bible (03). This document is the grammar those words slot into.*

---

## 1. The universal layer schema

Every prompt — static or a single video frame — is assembled from five layers. The layers are fixed; their contents are filled from the active Profile (01).

| Layer | Question it answers | Filled from |
|---|---|---|
| **L1 · Render & Camera** | How is this captured? lens, depth of field, medium | Profile F8 + the shot's needs |
| **L2 · Light & Energy** | How is it lit? source, direction, mood | Profile F4 + active Mode (F7) |
| **L3 · Subject & Action** | Who/what, doing what? | Profile F6 + Asset Bible (03) |
| **L4 · Environment & Context** | Where, in what world? | Profile F6 |
| **L5 · Composition & Negative space** | How is it framed? where does copy go? | Profile F8 + F9 |

**Assembly formula:**
```
[L1 Render/Camera] + [L2 Light/Energy] + [L3 Subject/Action] +
[L4 Environment] + [L5 Composition/Negative-space] +
[Negative block] + [Format spec]
```

The assistant builds left to right, taking one concrete choice per layer from the Profile's vocabulary. Where the Profile lists several options (casts, settings), the assistant picks one and can vary it across a series.

---

## 2. The negative block

Built from the Profile's **rejects** (F2, F5, F8, F10). It tells the engine what to exclude. Format depends on the engine (Doc 06), but the *content* is always the brand's forbidden list plus the universal floor:

```
universal floor: garbled text, watermark, extra fingers, distorted hands,
distorted faces, oversharpening, low-quality artifacts
+ brand rejects from the Profile (e.g. plastic skin, neon, flat studio light,
muddy color, dead-centre symmetry, generic stock look)
```

---

## 3. The negative-space rule *(fixes "always plain white")*

Negative space is **a real, defocused, in-palette region of the actual scene** reserved for copy — never a blank white panel dropped into the frame.

**The rule, every time:**
- It is part of the set: a soft-focused wall, a shadowed surface, an out-of-focus stretch of environment, an atmospheric haze — rendered in the Profile's negative-space fill colour (F9), not white.
- It is **low-contrast and low-detail** so type sits cleanly on top, but it still belongs to the scene's light and palette.
- The engine is told *where* it sits and *what it is*, e.g. "the left third is a soft-shadowed cream plaster wall, gently out of focus, holding clean negative space for copy."

**Treatment menu (pick one, in the brand palette):**
| Treatment | Looks like | Best for |
|---|---|---|
| Soft surface | defocused wall / plaster / fabric | editorial, product |
| Atmospheric | out-of-focus haze, bokeh, light gradient | cinematic, energetic |
| Shadow fall | a naturally shadowed corner of the set | moody, premium |
| Depth blur | far background thrown fully out of focus | macro, hero subject |

**Forbidden:** a flat white box, a hard-edged solid panel unrelated to the scene, a colour not in the palette. If the assistant is about to output "white space for text," it has drifted — stop and re-derive from this menu.

**Carry it through every copy-bearing frame.** Declaring the negative space once (in the master / first frame) is not enough — every still that will hold text must restate the reserved region in its own prompt. Tighter shots and re-framed angles otherwise fill the frame and leave nowhere clean for the headline. Across a static series or a video, each copy-bearing frame keeps the same *treatment* (repositioned per aspect, §5); frames that carry no copy (e.g. a tight macro insert) are the explicit exception and reserve nothing.

---

## 4. The scale system *(fixes "scale of things")*

Scale drift — a product that's hand-sized in one frame and table-sized in the next, or a subject floating at the wrong proportion — comes from leaving size implicit. The grammar makes it explicit on two axes.

### 4.1 Absolute anchor (how big the thing really is)
Every hero asset carries its **real-world dimensions** in its Asset Bible entry (03). The prompt anchors to that, e.g. "a 1-litre bottle, ~24 cm tall." The engine renders proportion correctly when given a real measurement and a reference object in frame.

### 4.2 Relative proportion (how big it sits in the frame)
State the subject's footprint and its relationship to other in-frame elements:
- "the bottle occupies the lower-right third, roughly the height of the adult hand beside it"
- "the player fills 60% of frame height; the floating balls read as foreground, ~1/3 their size"

### 4.3 Lens & distance anchor (the optics that set apparent size)
Apparent scale is set by lens + camera distance, so declare both (from L1):
- macro insert → "100mm macro, close, the cup fills the frame"
- environmental → "24mm, stepped back, subject small within the room"
Keeping the **lens family consistent across a series or scene** is what stops size from jumping between shots (see Docs 04, 05).

**Scale checklist for any prompt with a hero asset:**
1. Real dimension named (from 03)?
2. In-frame proportion stated (relative to hand / body / set)?
3. Lens + distance declared?
If all three are present, scale holds. If any is missing, it will drift.

---

## 5. Format & aspect mapping

| Output | Aspect | Note |
|---|---|---|
| Feed static / carousel | 4:5 | primary feed crop |
| Story / Reel / vertical video | 9:16 | reposition negative space to lower third |
| Landscape / web / hero | 16:9 | rare |
| Square legacy | 1:1 | only if a platform needs it |

The negative-space region (§3) must be repositioned per aspect — a side-third in 4:5 often becomes a lower-third in 9:16.

---

## 6. What a fully-assembled neutral prompt looks like

*Brand-neutral skeleton, before engine translation (Doc 06). Brackets are filled from the Profile + Asset Bible.*

```
[L1] [render medium], [lens] , [aperture], [depth of field].
[L2] [light source + direction + mood from Profile F4 / active Mode].
[L3] [subject from Profile F6 / locked asset from 03], [action], [texture from F5],
     [real dimension from 03].
[L4] [environment from Profile F6], [palette context from F3].
[L5] [composition from F8]; [negative-space region from F9, as a defocused in-palette
     surface — not white]; [in-frame proportion from §4.2].
[Negative block from §2]
[Format from §5]
```

This skeleton never changes. Only the bracketed contents do — which is what lets one engine serve every brand.

---

*Doc 02 of the Art Direction Engine. Brand-neutral. Reads its contents from 01 and 03.*
