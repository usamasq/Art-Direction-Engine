# Modular AI Visual System — 06 · Engine Adapters

*The final translation step. Takes the brand-neutral prompt assembled by the Grammar (02) and renders it in the correct syntax for the chosen engine. Also specifies how each engine achieves the consistency the Asset Bible (03) and Video module (05) call for. One job → one recommended engine → that engine's syntax.*

> Current as of mid-2026. The model landscape changes monthly — re-verify versions before a major campaign.

---

## 1. Choosing the engine

| The job | Recommended engine | Why |
|---|---|---|
| Brand-safe stills at volume, consistent color/material | **Flux 2 Pro** | holds look across many outputs cheaply |
| Product/character held identical across scenes (hero & derived stills) | **Nano Banana Pro** (Gemini 3 Pro Image) | best multi-image fusion + cross-scene consistency; session memory; "thinking" mode |
| Quick, throwaway scene / environment reference stills | **Nano Banana** (standard, Gemini 2.5 Flash Image) | fast and cheap for refs that won't be hero frames |
| AI renders the headline text in-image | **GPT Image 2** | best in-image text + conversational edits |
| Atmospheric, cinematic stills with reference + style | **Midjourney V7** | strongest mood; `--oref` + `--sref` |
| Crisp typography / poster / vector layout | **Ideogram 3 / Recraft V3** | type and vector leaders |
| Non-Latin / Arabic in-image text | **Qwen Image** | best non-English text handling |
| **Video** — native synced audio + multi-shot continuity + first/last-frame | **Gemini Omni** (Omni Flash today) | native audio in one pass; **stateful multi-turn editing**; native first/last-frame; the new center of Google's video stack |
| **Video** — strongest single-shot character fidelity (no session continuity) | **Seedance 2.0** | up to ~9 refs per generation; higher raw consistency, but can't carry it across an editing session |
| **Video** — camera control, repeatable ad look | **Runway Gen-4.5** | director control + consistency |
| **Video** — cheap high-volume iteration | **Kling 3.0** | lowest premium cost, solid 4K |

> ℹ️ **"Google Omni" = Gemini Omni** (Google I/O 2026, May 19). Google is folding the standalone **Veo** line into the core Gemini system; Omni is the successor and the default video pick here. Omni Flash currently caps clips at **10 seconds** (longer with Omni Pro) — plan scenes as ≤10s shots.
> ⚠️ **Do not build on Sora** — OpenAI discontinued the app (April 2026); API ends September 2026.
> ⚠️ **DALL·E 3 is retired** (May 2026) — replaced by GPT Image 2.

---

## 2. Stills — syntax & consistency per engine

### Midjourney (V7 default; V8.1 available)
- **Syntax:** prompt text, then flags. `--ar [aspect] --style raw --v 7`
- **Asset lock:** **Omni Reference** — `--oref [IMAGE_URL] --ow [0–100]` (dial `--ow` down to ~70 for more scene flexibility). *Replaces the old `--cref`/`--cw`.*
- **Style lock:** `--sref [code] --sv 6`
- **Negative block:** `--no [comma-separated rejects]`
```
[neutral prompt body] --no [rejects] --oref [ASSET_URL] --ow 90 --sref [BRAND_CODE] --style raw --ar 4:5 --v 7
```

### Nano Banana Pro (Gemini 3 Pro Image) — hero & derived stills
- **Syntax:** natural language; no flags. Multi-reference formula: **[reference images] + [relationship instruction] + [new scenario]**.
- **Label every reference's role in the prompt.** The single biggest consistency lever: tell it what each image is *for* — e.g. "image 1 = product, preserve label, shape and colour; image 2 = scene/background; image 3 = lighting." Unlabelled references make the model guess what to keep.
- **Cap references at ~6, front-load the critical 2–3.** More is *worse* — past ~6 images structural accuracy degrades. Put the must-hold elements (the product, the master frame) in the first 2–3 slots; reserve the rest for subtle style.
- **Session memory = the master-frame method, built in.** Define the asset fully in the first prompt of a session; later prompts in the *same session* need only describe the action/angle — the model recalls the locked asset. So derive all of a scene's stills in **one session** (see 05 §5).
- **Use "thinking" mode** for hero/derived stills (it drafts interim compositions before the final), and state negatives in prose ("no deformed hands, no plastic sheen, no white panels"). Wrap any required in-image text in quotes with font/position.

### Nano Banana (standard, Gemini 2.5 Flash Image) — quick reference stills
- Fast and cheap; use for throwaway **scene/environment reference** images that won't be hero frames. Promote to **Pro** for anything that must hold fidelity across the video.

### GPT Image 2
- **Syntax:** natural language; conversational editing.
- **Asset lock:** supply the reference; ask it to keep the asset intact while changing the scene. Best when the headline text must render in-image.

### Flux 2 Pro
- **Syntax:** natural language; supports reference + edit (Flux Kontext) for iterative changes.
- **Asset/style lock:** reference image + consistent seed; reliable color/material across volume.

### Qwen / Ideogram / Recraft
- **Qwen:** when in-image non-Latin text is unavoidable.
- **Ideogram / Recraft:** when the layout/type is generated rather than composited.

---

## 3. Video — syntax & consistency per engine

### The atomic rule (all video engines)
A video model only keeps the product/world consistent for **what's in the still you hand it**. So always work **one still → its animation, motion-only**: supply an approved still, and prompt only how it *moves* — never re-describe the product, set, or light (already locked in the still). Never generate the scene or product from text. And because a new camera angle isn't in the reference frame, **each angle needs its own still** — multi-angle coverage = one still per angle, each animated separately (Video module 05 §4.1, §5).

### First-and-last-frame control *(two cases — subject arc OR large camera move)*
Supply **both** a start still and an end still and let the model interpolate when either is true: (a) a single shot has a clear before/after **subject** arc (hand grabs product, pour, door opens); or (b) the shot has a **large camera move** (orbit, big push-in, jib, whip) — the start frame doesn't contain the far side of the subject or the geometry the camera moves toward, so one still can't drive it. Small camera moves and ambient motion animate fine from one still. **Gemini Omni supports first/last-frame natively**; also on current Runway / Kling — confirm in the engine's UI.

### Gemini Omni (Omni Flash) — default video engine
- **Syntax:** natural-language brief + explicit **audio cues** (dialogue, SFX, ambient) + labelled inputs. No `--` flags; describe slow-motion in words. The recommended brief has five parts: **Goal · Input role · Scene · Motion · Constraints.**
- **Label each input's job** (same rule as the stills): "use the attached still as the product/scene reference — preserve it; animate only the motion below." Reference defines appearance; the prompt defines movement.
- **Stateful multi-turn editing — its superpower.** The scene *remembers* prior turns, so for a multi-shot sequence you can build forward instead of regenerating. **Change one thing per turn:** a camera reposition is its own turn; a style change is its own turn; don't bundle outfit + background + camera + product rotation into one instruction or drift becomes undiagnosable.
- **Native first/last-frame** for two-state shots and large camera moves. **10s clip cap** (Omni Flash) — keep each shot ≤10s.
- **Use for:** any shot needing native sound (ASMR pour, crowd roar) and any multi-shot scene needing continuity across cuts.
```
Goal: 10s premium product hero clip.
Input role: attached still = the product+scene reference — preserve exactly, animate only the motion.
Scene: the open honey jar beside a warm dish on a worn oak board, glossy amber catching firelight.
Motion: a wooden dipper lifts and drizzles a thick glossy ribbon of chili honey over the dish; slow pan right→left.
Constraints: keep label, shape and colour exact; no added text; realistic viscous flow.
Audio: a soft sizzle, the low crackle of a nearby hearth.
```

### Runway Gen-4.5 — when you want explicit camera/motion-brush control
- Natural language + camera direction (push-in, pan, motion brush); strong reference consistency. Animate the master/derived stills. Good alternative when Omni's continuity isn't needed but precise camera control is.

### Kling 3.0
- Cheap high-volume iteration; solid 4K, good macro physics.

### Seedance 2.0 — when single-shot fidelity matters more than continuity
- Up to ~9 references per generation, higher raw character consistency — but **no stateful session continuity**, so it won't carry a look across an editing sequence. Use for a standalone hero shot, not a multi-turn scene.

---

## 4. Translation example — one neutral prompt, three engines

**Neutral (from the Grammar, 02 §6):**
> 100mm macro, shallow DoF. Low warm side light, soft-edged shadows. An 8cm amber chili-honey jar [locked asset], a wooden dipper lifting a thick glossy ribbon of honey over a warm dish; chili flecks suspended in the amber. Worn oak board, dark hearth-lit kitchen, warm amber-and-char palette. Asymmetric; the left third is a soft-shadowed charcoal plaster wall, defocused, holding negative space; the jar fills the lower-right, ~half the frame height. Negative block. 9:16.

**→ Midjourney V7:**
```
100mm macro, shallow depth of field, low warm side light, soft-edged shadows,
a wooden dipper lifts a thick glossy ribbon of amber chili honey over a warm dish,
chili flecks suspended in the honey, worn oak board, dark hearth-lit kitchen,
warm amber-and-char palette, asymmetric composition, defocused charcoal plaster
wall left third for negative space
--no plastic sheen, neon, flat studio light, white panel, distorted hands, watermark
--oref [JAR_SHEET_URL] --ow 90 --sref [BRAND_CODE] --style raw --ar 9:16 --v 7
```

**→ Nano Banana Pro (labelled references, one session):**
```
image 1 = the honey jar reference (preserve label, shape, colour exactly);
image 2 = the hearth-lit kitchen master frame (preserve set + light).
Relationship: place the jar from image 1 into the scene of image 2.
New scenario: 100mm macro — a wooden dipper lifts a thick glossy ribbon of chili honey
over the warm dish, amber catching the firelight. Left third stays a defocused charcoal
plaster wall for copy (not white). No deformed hands, no plastic sheen. Vertical 9:16.
```

**→ Gemini Omni (animating the approved still — labelled, motion-only):**
```
Goal: animate the attached still into a 10s macro clip.
Input role: the still is the product+scene reference — preserve it exactly, animate only the motion.
Motion: slow-motion — the dipper finishes lifting and a thick glossy ribbon of honey drizzles
over the dish; an ember glows behind. Camera holds with a slight pan right→left.
Constraints: keep label/shape/colour exact; realistic viscous flow; no added text.
Audio: a soft sizzle, the low crackle of a hearth.
```

Same intent, three syntaxes — which is exactly why engine translation is its own module.

---

*Doc 06 of 7. Always the last step. Brand-neutral.*
