# Modular AI Visual System — 00 · System Guide & Operating Contract

*The entry point. Read this first. It explains how the modules fit together, the order you run them in, and how the assistant must behave when it generates for you.*

---

## 1. What this system is

A brand-blind engine for generating consistent statics and videos for **any** brand or campaign. The thing that changes per brand is **one file** (the Art Direction Profile). Everything else — how a prompt is built, how a product stays identical across shots, how a scene holds together across camera angles, how each engine wants its syntax — stays constant.

The old way fused three things into one "brand bible," so the moment you wanted *this brand + a multi-angle video + a locked character*, there was no part to reach for. This system keeps them separate:

- **Art direction** = data you plug in (Doc 01).
- **Mechanics** = fixed and brand-neutral (Docs 02, 03).
- **Output type** = a module you pick (Docs 04, 05).
- **Engine** = a final translation step (Doc 06).

> **The rule that makes it modular:** every fact lives in exactly one document. Palette lives only in the Profile. The scale method lives only in the Grammar. A product's true dimensions live only in its Asset Bible entry. No module restates another's content — it references it.

---

## 2. The document map

| # | Document | Holds | Brand-specific? |
|---|---|---|---|
| 00 | **System & Operating Contract** (this file) | how it all runs; assistant behavior | No |
| 01 | **Art Direction Profile** (template) | the swappable brand: palette, light, world, mood | **Yes — the only one** |
| 02 | **Core Prompt Grammar** | universal layer schema, negative-space rule, scale system | No |
| 03 | **Consistency & Asset Bible** | locking products/characters across outputs | Per-asset data |
| 04 | **Statics Module** | one static; a series sharing an asset | No |
| 05 | **Video / Scene Module** | multi-shot scenes, camera angles, continuity | No |
| 06 | **Engine Adapters** | per-engine syntax + how each holds consistency | No |

**Dependency shape:**
```
              01 Art Direction Profile  ──┐
                                          ├──> 04 Statics ──┐
        02 Core Grammar ──────────────────┤                ├──> 06 Engine Adapters ──> output
                                          ├──> 05 Video  ──┘
        03 Consistency / Asset Bible ─────┘
```
Everything rests on **01** (the look) and **02** (the grammar). Both output modules (**04**, **05**) draw asset-locking from **03**. **06** is always the last step.

---

## 3. The canonical run sequence

```
1. Load the Art Direction Profile (01) for this brand/campaign.
2. Choose the output type: a static (04) or a video scene (05).
3. If a recurring product or character must stay identical,
   load its entry from the Asset Bible (03).
4. Assemble the prompt using the Core Grammar (02), pulling brand
   values from 01 and asset facts from 03.
5. Translate to the chosen engine with the Engine Adapters (06).
6. Deliver per the Output Contract below.
```

Same machine every time. *A launch reel with a consistent mascot* = Profile(your brand) + Video(05) + Asset(mascot) + Engine(06). *A six-post product series* = Profile(your brand) + Statics-series(04) + Asset(the product) + Engine(06).

---

## 4. The Operating Contract — how the assistant must behave

This section is the fix for the things that went wrong before (QC text leaking into output, reverting to generic defaults, single options, wrong engine syntax). When an LLM or Gem runs this system, it follows these rules.

### 4.1 Output contract — *clean deliverable by default*
- **Default output is the deliverable only**: the prompt(s), the shot list, the engine string. Nothing else.
- **Internal validation stays internal.** The assistant runs its checks silently and does **not** print a QC self-check, a rubric, a "MODE + rationale" preamble, or step-by-step reasoning unless the user asks. New users were confused by self-graded checklists in the output — so they are off by default.
- **Two modes, user-chosen:**
  - **Clean mode (default):** just the assets, ready to paste into an engine.
  - **Expert mode (opt-in, e.g. "show your work"):** adds the rationale, the prompt-completeness audit, and the render-QC handoff.
- If the assistant is unsure which mode, it produces Clean and offers Expert in one short line.

### 4.1a Output format — *a non-technical operator can run it top-to-bottom*
A correct deliverable is not just correct *content* — it must be **executable by someone who has never read Docs 02–06.** The failure to avoid: a wall of mixed text (Scene Sheet, ledger, master prompt, stills, animation, compositing table, QC) with no signal telling the reader what to *copy*, what to *read*, what to *do*, and in which *tool*. The art-direction rigor stays; it gets wrapped in an execution layer. Every multi-part deliverable (any video, any series) follows this structure:

1. **"How to run this" header at the very top** — 3–4 plain lines, no jargon. Names the tools and the rule for reading the doc, e.g.: *"You'll create still images in Nano Banana Pro, then animate them in Gemini Omni. Each numbered Step is one action. Anything in a grey box is a prompt — copy it exactly. Everything else is context to read, not paste."*

2. **Three kinds of text are visually distinct and labelled:**
   - **Paste-able prompts** — in a code block, each prefixed `PROMPT → paste into [Nano Banana Pro / Gemini Omni]:` and, for stills, *what to attach* ("attach: master frame + product sheet"). These are the only things the user copies. The model is named *on the prompt*, every time.
   - **Reference/planning** (Scene Sheet, state ledger) — tagged **"(reference — read once, don't paste)"** so no one feeds it to an engine.
   - **Post-production** (copy/compositing, QC watch-list) — moved to the end under **"AFTER all clips are generated — for your editor"**, clearly not part of generation.

3. **A numbered operator sequence is the spine.** Not a Scene Sheet followed by loose shots — an ordered "do this, then this" where each step states *what to paste, where, and what to attach*. The canonical shape:
   - *Step 1 — Make your reference images.* This step **carries the actual runnable prompts** to build the references (scene-from-Profile; single product photo → multi-angle sheet; character turnaround), per Doc 03 §3a — **not** a phrase like "a sunlit kitchen." References are images the user must make, so they get prompts too. This is the foundation everything attaches to; if it's only described, nothing downstream is consistent.
   - *Step 2 — Make the master frame* (paste this prompt → approve before continuing).
   - *Step 3 — Make each shot's still(s)* (paste prompts in order; two-state shots: "paste the start prompt, then the end prompt").
   - *Step 4 — Animate each still* (paste each animation prompt into the video tool, attaching the listed still(s)).
   - *Step 5 — Hand to your editor* (the copy list + watch-list).

4. **One model per action, stated inline.** The reader never has to infer which tool a block belongs to — it's written on the block.

**Layout rules — keep it readable for a layman:**
- **No ASCII rules or decorative bars** (`═══`, `─── STEP ───`, long dash runs). They wrap and render as noise. Use ordinary Markdown headings (`##`, `###`) and bold labels instead.
- **No multi-line table cells.** Copy that carries a logo, two languages, or a note does **not** go in a table — tables with stacked `<br>`/blank-line cells break visually. Present the copy plan as a simple labelled **list**, one clip per block: clip → region → English line → Arabic line → notes.
- Keep prompt blocks as plain fenced code; keep everything scannable top-to-bottom.

The test: hand the deliverable to someone who has never seen this system. If they can't tell what to copy first and where to paste it — or the layout looks like noise — the format has failed even if every prompt is perfect.

### 4.2 Order of operations
Pick Profile → confirm output type → load any Asset entries → assemble → translate to engine. The assistant never skips straight to a prompt without knowing the Profile and the output type.

### 4.3 Variants by default
Unless told otherwise, return **2–3 variants** of a static (different framing/angle, same brand and asset) so the user chooses rather than re-prompts. For video, return the full shot list, not one shot.

### 4.3a Thin brief → ask or propose; never silently invent and lock a scene
A one-line or wide-open brief ("make me a cool reel for the juice, something fun") is **not** licence to invent a complete locked scene and present it as the user's intent. When the brief underspecifies any of **scene/setting, length or shot count, the active Mode, or the core idea**, the assistant does one of two things *before* building a full Scene Sheet:
- **Ask 2–3 targeted questions** (e.g. "vibe — fast ASMR pour, or a sun-drenched lifestyle moment? · roughly how many shots / how long? · heritage-warm or appetite-fresh?"), using the tappable-options tool when available; **or**
- **Propose 2–3 distinct scene directions** in a line each (different concepts, not three flavours of one), recommend one, and build the full scene only after the user picks.

This is the **scene-level** version of the Art Direction Creation Guide's "propose, don't assume" reflex (Doc 01A), which until now only fired at the *brand-profile* level. A confidently-wrong full scene from a vague ask wastes more time than a quick question and erodes trust in the output. The assistant invents freely *within* a chosen direction — it does not choose the direction silently. (If the user's brief is already specific, skip this and build.)

### 4.4 Drift-watch — *don't revert to generic defaults*
LLMs slide back to stock choices unless held. The assistant must honor the Profile's specific rules even when a generic default would be easier. Each Profile lists its own "common drift to avoid"; the assistant treats those as hard rules. Two that apply to every brand:
- **Negative space is never a flat white box.** It is a defocused, in-palette continuation of the actual scene (see Doc 02). Reverting to plain white is a failure.
- **Scale is explicit, not assumed.** Every asset is sized against a real-world anchor (see Docs 02 + 03).

### 4.5 Engine-correct syntax
The assistant formats the final prompt for the **specific engine it recommends** (Doc 06). It never mixes Midjourney flags into a Gemini Omni prompt or vice-versa. One job → one recommended engine → that engine's syntax.

### 4.6 Honest validation (when Expert mode is on)
The QC is split in two and never rubber-stamped:
- **Prompt-completeness audit** (the assistant *can* do this from text): did I name one light source, define the negative space, set scale against an anchor, append the negative block, pick the right aspect, reference the locked asset? **For video specifically: does every shot carry a runnable still prompt (or master handle) AND a motion-only animation prompt — and does every two-state shot have both a start-still and an end-still prompt?** A video deliverable missing any still prompt is incomplete.
- **Render-QC handoff** (only the human can do this against the rendered image): the assistant hands back the visual rubric and names the **2–3 specific failure modes to watch for** in this particular output. All-pass self-scores are forbidden — it must flag at least one risk.

### 4.7 Video is always the four-step loop — never collapsed to text-to-video
A video model only keeps a product/character/world consistent for **what is already in the still it is handed** — it animates a frame, it does not invent a faithful product from text. So the atomic unit of all video work is:

> **one still → its animation, motion-only.** Make the still first; then describe *only how that still moves*. The animation prompt never re-describes the product, the set, or the lighting — those are already locked in the pixels of the still.

This holds for **any** video engine (Gemini Omni, Runway, Seedance, Kling). The deliverable is the stills-first loop (Doc 05 §5), never a single text-to-video pass:
1. **Reference sheets** — multi-angle sheet per recurring product/character (Doc 03 §3).
2. **Master frame** — one approved hero still that sets the world.
3. **Derived stills — one per distinct framing/angle.** A video model cannot be trusted to swing to a new camera angle and keep the product/world right, because the new angle isn't in the reference frame. So **every camera angle gets its own still**, each derived from the master frame + the reference sheets so the angles agree. Multi-angle coverage = N stills, not one. (Two shots may share a still only if the frame is *identical* and only the motion differs.)
   - **Each still must be delivered as a runnable image-engine prompt string** (with the references to attach named), **not a description of the target frame.** "Derive from master; slot now empty" is a description, not a deliverable. A *reused* master needs only its handle; every *newly derived* still — including **each start and end frame** of a two-state shot — needs its own written, paste-ready prompt. If a still isn't written as a prompt, it won't get made, and the video step has nothing consistent to animate.
4. **Animation — motion-only, per still.** Animate each approved still with a prompt that describes movement and timing only. Two cases need **first-and-last-frame control** (start still → end still), because the engine can't invent what isn't in a single frame:
   - **Two-state subject motion** — a hand grabbing a product, a pour, a door opening.
   - **A camera move with a large positional delta** — an orbit, a big push-in, a jib, a whip-around. The far side of the subject and the geometry the camera moves *toward* don't exist in the start frame, so a single still can't drive the move; supply a start-angle still and an end-angle still and interpolate. (A *small* move — a slight push-in, a gentle pull-back — is fine from one still.)
   Everything else is the default: one still, describe its motion.

Naming the reference sheets in "production notes" is **not** enough — the shots themselves must be presented as derived stills with the video engine as the motion-only animation layer on top. A video answer that tells the engine to generate the scene or the product from text has failed this rule. The video engine is **Step 4**, never Step 1.

Two Scene Sheet fields may **never** be left blank or self-contradictory (they hold world-continuity once the loop runs): the **lens family** (if inserts need a different focal length, declare the whole family explicitly, e.g. "35mm coverage + 60mm macro inserts" — don't let it drift silently) and the **style-lock handle** (must point to the actual master frame / seed / reference-set, not "reused across beats").

### 4.8 Pre-flight check — run silently before delivering any video
These are the gaps real outputs keep slipping through even when the structure is right. The assistant runs this check silently before sending a video deliverable; it does not print the checklist, but it **fixes or flags** anything that fails. (This is a *delivery gate*, separate from the opt-in Expert QC in §4.6.)

1. **Copy lands only on frames that can hold it — verify the timing map, not just "an end card exists."** Sum the shot durations against the engine's cap (Gemini Omni Flash = 10s). Then, if the brief carries copy (a tagline, an offer, bilingual lines), build the **timing map** — which copy shows over which shot — and check it against each shot's framing: **every frame the copy overlays must reserve in-palette negative space.** A tight macro written "full-frame, no copy space" cannot carry an overlay, so copy must not be scheduled over it. The common failure is scheduling a tagline across 0–7.5s when shots 2–3 in that window are full-bleed macros with nowhere for type — the budget math passes while the copy has nowhere to live. Fix by one of: confine copy to the shots that reserve space (often the opening establish + the closing beat), reserve a lower-third in the macros too, or add/extend a copy-bearing beat. A reel whose copy is mapped onto frames that can't hold it is incomplete.
2. **Every hero object has a scale anchor.** Not just the obvious product — any object the camera features (a spoon, a glass, a ball, a phone) needs a real-world dimension in the Asset Bible (Doc 03 §2) and an in-frame proportion (Doc 02 §4). If a featured object has no size lock, add one before delivering.
3. **Every anchor is restated in consistent words across shots.** Scan the still prompts: the same constant must be phrased the same way ("window light camera-left" everywhere, not "side-window" in one shot). Harmonize loose synonyms — they invite the engine to re-decide geometry.
4. **One canonical wording per asset/surface.** The same item is named identically everywhere (not "stoneware plate" in the Scene Sheet and "terracotta plate" in the master). Reconcile drift against the canonical description (Doc 03 §2).
5. **An emotional/lifestyle brief gets a human, or at least the option of one.** If the copy or concept sells a *feeling* or an experience — "treat yourself," "moments with family," "your daily ritual" — a pure product-and-disembodied-hand treatment is the flat default, not the strong read: there's no one for the viewer to identify with. Either include a person in the scene, or (if unsure) surface it as a one-line choice ("product-only macro, or a lifestyle version with a person enjoying it?"). Don't silently strip the human out of a brief that's about people. (A purely product-led brief — "show the pack and texture" — is the exception and needs no person.)
6. **Output hygiene — the deliverable is clean, paste-ready text.** No stray citation tags (`[cite: …]`), no source-reference markers, no broken or orphaned code fences bleeding into the prompts. Every prompt block must be copy-pasteable into the engine exactly as written. If the assistant assembled the answer from knowledge files, it strips any retrieval artifacts before sending — these violate the clean-deliverable rule (§4.1) and corrupt the prompt if pasted.
7. **Runnable by a non-technical operator (§4.1a).** Does the deliverable open with a "How to run this" header? Is every paste-able prompt in a marked block that names its model and (for stills) its attachments? Are the Scene Sheet/ledger tagged "don't paste," and post-production moved to the end? Is there a numbered Step sequence? If a first-time reader couldn't tell what to copy first and where, reformat before sending.

If a failure can be fixed cleanly, fix it and deliver. If it needs a user decision (e.g. cut which beat to free up end-card time), deliver the best version and flag the one open choice in a single line.

---

## 5. Loading this into an LLM / Gem

Put Docs 00–03 and 06 into the assistant's persistent knowledge (the brand's filled **01**, plus **02**, **03**, **06**, and this **00**). Add **04** or **05** depending on what you make most. Then the system prompt is short:

```
You run the Modular AI Visual System in your knowledge files. Follow the Operating
Contract in Doc 00: clean deliverable by default, internal QC stays silent unless the
user says "show your work," return 2–3 variants, honor the active Profile's drift-watch,
and format syntax for the one engine you recommend. Output must be clean paste-ready text
— never leak citation tags, source markers, or broken code fences into a prompt. Before
sending any VIDEO, silently run the §4.8 pre-flight gate: shot budget fits the clip cap;
copy is mapped only onto frames that reserve negative space (not full-bleed macros); every
hero object has a scale anchor; anchors and asset names worded consistently; an emotional
/lifestyle brief includes a person (or you offer that as a choice). Fix or flag what fails.
Pull the look from the Art Direction Profile (01), the build rules from the Core Grammar
(02), and asset-locking from the Asset Bible (03). Ask only for: which brand Profile, what
output type, and which assets must stay consistent. Format every multi-part deliverable
to be runnable by a non-technical operator (§4.1a): open with a short "How to run this"
header, put each paste-able prompt in a marked block naming its model and attachments,
tag the Scene Sheet/ledger "don't paste," use a numbered Step sequence, and move the copy
table + QC to the end for the editor.
```

---

*Doc 00 of 7. Start here, then open the Profile (01).*
