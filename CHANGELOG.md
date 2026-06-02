# Changelog

All notable changes to the Art Direction Engine.

## [1.2.0] — 2026-06-03

### Added
- README **"Range — the same system, different worlds"** showcase: two extra fictional
  brands rendered as 3-image static series — **Kestra** (sporty luxury / footwear) and
  **Vespra** (premium minimalist / fragrance) — demonstrating that swapping only the
  Profile retargets the whole system while each brand stays internally consistent.
- Six showcase renders under `assets/examples/` (`kestra_post1-3`, `vespra_post1-3`),
  documented in the assets slot table. These two brands are README-only (no worked-example
  docs by design).

## [1.1.0] — 2026-06-03

### Added
- `SETUP.md` — a non-technical "build your own AI Art Director" walkthrough: create a
  Profile, set up the assistant (Claude Projects / custom GPT / Gemini Gem) with a
  copy-paste system prompt, run a first job, and troubleshoot.
- **Typography support** as a first-class **copy mode**: Profile **Field 13** (brand type
  spec) plus Grammar **§3a** defining **Reserve** (background only; type composited in
  post in the real font — default) vs **Render** (engine sets an approximate headline
  in-image via a text-capable engine). Wired through Statics (04), Video (05),
  Engine Adapters (06), and the Operating Contract (00). Works for stills and video;
  logos and legal text are always composited.

### Changed
- Reframed history/insider phrasing in Doc 00 (e.g. "the old way", "new users were
  confused", "until now") to describe general principles a first-time reader can follow.

## [1.0.0] — 2026-06-03

First public release. Restructured a private art-direction system into a brand-blind,
publishable toolset.

### Added
- `README.md` landing page with a Mermaid dependency diagram and full repo map.
- `START_HERE.md` onboarding guide with the video production-loop diagram and
  LLM-loading instructions (Claude Projects / Gemini Gem / custom GPT).
- `examples/` — a complete fictional teaching brand, **Ember & Comb** (craft chili honey):
  a filled Profile with Creation-Guide rationale, and a full runnable video deliverable.
- `assets/` — captioned image slots for example renders.
- `.gitignore` — keeps the private/ folder (real client work) out of the repo.

### Changed
- Moved the eight toolset modules into `docs/`.
- Scrubbed brand-specific fingerprints from the generic docs so the toolset reads
  fully brand-blind; replaced the Profile template's worked example with the fictional brand.

### Notes
- Engine list (Doc 06) reflects a mid-2026 snapshot and is meant to be re-verified
  before a major campaign.
- No LICENSE file committed yet; release is intended as CC0 (public domain).
