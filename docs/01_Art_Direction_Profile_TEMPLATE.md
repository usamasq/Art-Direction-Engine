# Modular AI Visual System — 01 · Art Direction Profile (Template)

*The one swappable file. This is the only document that changes per brand or campaign. Copy it, fill every field, name it for the brand (e.g. `01_Profile_AlKhamayil.md`), and the other six modules will run on it unchanged.*

> **How the rest of the system uses this:** the Core Grammar (02) has empty slots — Light, Palette, Subject, Environment, Negative-space. Those slots are filled from the fields below. Swap this file and the whole system retargets.

---

## How to fill it
- Be concrete. "Warm light" is a slot the engine fills with a cliché; "low-angle late-afternoon sun through a side window, soft-edged shadows" is direction.
- Give **hex values**, **real descriptions**, and **explicit rejects**. The rejects matter as much as the targets — they become the negative block.
- Leave nothing as "(brand default)". If a field doesn't apply, write `n/a` so it's a decision, not an omission.

---

## FIELD 1 — Brand snapshot
- **Brand / campaign:** `____`
- **One-line positioning:** `____`
- **Audience:** `____`
- **What the visuals must make a viewer feel / do:** `____`

## FIELD 2 — The anti-aesthetic (Reject → Target)
*The single most useful field. Defines the look by contrast.*
- **Reject (the generic version we refuse):** `____`
- **Target (our standard):** `____`

## FIELD 3 — Palette
*Roles matter more than names — the Grammar references roles ("base", "accent", "negative-space fill").*
| Role | Name | Hex |
|---|---|---|
| Canvas / base | `____` | `#____` |
| Accent 1 | `____` | `#____` |
| Accent 2 | `____` | `#____` |
| Neutral / negative-space fill | `____` | `#____` |
| Special / prestige (optional) | `____` | `#____` |
- **Saturation stance:** `muted / balanced / vibrant` → `____`
- **What each accent *means* (so it's used with intent):** `____`

## FIELD 4 — Lighting signature
- **Primary light:** `____` (source, direction, time of day, hardness)
- **Mood of shadows:** `____`
- **Forbidden lighting:** `____` (e.g. flat multi-source studio floods)

## FIELD 5 — Texture & materials
- **Mandated textures (the tactile truth):** `____`
- **Surface finish bias:** `matte / satin / glossy` → `____`
- **Forbidden surface looks:** `____` (e.g. plastic skin, CGI sheen)

## FIELD 6 — Subject / world vocabulary
*The casting and set dressing. Lists, not single options — the system rotates through them.*
- **People / cast (roles, wardrobe, demeanour):** `____`
- **Settings / environments:** `____`
- **Signature props / hero objects:** `____`
- **Cultural / regional precision rules (avoid generic descriptors):** `____`

## FIELD 7 — Mode dial (declare 1–N modes)
*A brand can have one look, or a few it switches between by content type. Declare each as a named mode so the assistant picks the right one per asset.*
| Mode name | Use it for | Light | Color energy | Texture/feel |
|---|---|---|---|---|
| `____` | `____` | `____` | `____` | `____` |
| `____` | `____` | `____` | `____` | `____` |
- **Rule for which mode applies to which content:** `____`

## FIELD 8 — Composition defaults
- **Framing bias:** `____` (e.g. asymmetric, rule-of-thirds, subject off-centre)
- **Depth of field:** `____`
- **Forbidden:** `____` (e.g. dead-centre static symmetry)

## FIELD 9 — Negative-space treatment
*Solves the "always plain white" problem at the brand level. Define what the copy area actually looks like.*
- **Negative space is:** a defocused, in-palette continuation of the scene — **never a flat white box**.
- **Default fill for this brand:** `____` (e.g. soft-shadowed cream plaster wall; out-of-focus glowing haze)
- **Where it usually sits:** `____` (note RTL/LTR needs if bilingual)

## FIELD 10 — Hard constraints (never-do)
- `____` (e.g. no real identifiable people; no neon; no minors in any sexualised framing; no competitor cues)

## FIELD 11 — Drift-watch (this brand's common failure modes)
*Listed so the assistant treats them as hard rules, per the Operating Contract §4.4.*
- `____`
- `____`

## FIELD 12 — Style-lock handles (filled in once you've locked a look)
*Reused across the whole campaign for feed cohesion. Engine specifics live in Doc 06.*
| Mode | Midjourney `--sref` | Seed / reference-set ID |
|---|---|---|
| `____` | `____` | `____` |

---

## APPENDIX — Worked example (Ember & Comb, abridged)
*Shows what "filled" looks like, using the fictional teaching brand. A real profile fills every field; this is condensed. The full version lives in [`examples/profile_EmberAndComb.md`](../examples/profile_EmberAndComb.md).*

- **F1 Positioning:** "Honey with a bite" — a small-batch chili honey for people who drizzle it on everything.
- **F2 Reject:** bright supermarket-condiment gloss, clinical white studio packshots, cartoon-chili mascots, sticky pastel cuteness, flat even lighting. **Target:** hearth-lit craft still-life — one warm low light source, glossy amber against char-dark surfaces, real food, real hands.
- **F3 Palette:** base Charcoal `#2A2422`; accents Amber-honey `#C8841E`, Ember-red `#9E3B22`; negative-space fill Warm Ash `#D8CFC2`; special — Beeswax-gold `#E6B964`. Saturation: rich but warm, never neon. Amber = the honey; ember-red = the chili heat.
- **F4 Light:** single low warm light from one side — hearth/firelight or a low dusk window; soft-edged shadows, gentle glow. Forbidden: flat multi-source studio floods, cold daylight.
- **F5 Texture:** glossy viscous honey, suspended chili flecks, raw honeycomb, worn oak, cast iron, linen. Glossy on the honey, matte everywhere else. Forbidden: plastic sheen, CGI gloss on surfaces.
- **F6 World:** cast — a cook's hands, a friend reaching across a table, a small gathering; settings — a dark rustic kitchen, a hearth, a worn dining table; props — the honey jar + wooden dipper, warm food (fried chicken, a cheese board, warm biscuits), cast iron. Avoid generic "foodie flatlay".
- **F7 Modes:** *Hearth* (warm, dark, intimate — brand & story posts) · *Drizzle* (tighter, glossier, appetite-forward macro — product/craving posts).
- **F9 Negative space:** soft-shadowed charcoal plaster wall or out-of-focus warm-dark kitchen; never plain white.
- **F11 Drift-watch:** honey reading thin/runny instead of thick and glossy; warmth tipping into orange oversaturation; losing the chili "heat" cue so it reads as plain honey; defaulting to bright overhead foodie-flatlay light.

---

*Doc 01 of 7. Filled per brand. Feeds every other module.*
