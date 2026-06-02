# Assets

Visual references for the repo. Two kinds live here:

1. **Diagrams** — the flow/dependency diagrams in the README and START_HERE are written as [Mermaid](https://mermaid.js.org/) and render directly on GitHub, so they need no image files.
2. **Example renders** — the slots below. The worked example ([`../examples/worked_reel_EmberAndComb.md`](../examples/worked_reel_EmberAndComb.md)) gives you the exact prompts; render them in your image/video tools and drop the results in [`examples/`](examples/) here so readers can see the system's output, not just read about it.

> All example imagery should be from the **fictional** Ember & Comb brand (or another fictional brand). Keep real client renders out of the public repo.

## Slots to fill — Ember & Comb "The Drizzle" reel

Render from the prompts in the worked example and save with these names in [`assets/examples/`](examples/):

| Filename | What it should show | From |
|---|---|---|
| `ember_scene_ref.png` | The empty dark-kitchen scene plate | Step 1a |
| `ember_jar_sheet.png` | The jar multi-angle reference sheet | Step 1b |
| `ember_master_frame.png` | The approved hero still (board + chicken + jar) | Step 2 |
| `ember_shot2_end.png` | Dipper lifted, first amber ribbon falling | Step 3, Shot 2 |
| `ember_shot3_macro.png` | Macro — honey landing, chili flecks | Step 3, Shot 3 |
| `ember_shot4_reach.png` | Someone reaching in, honey thread | Step 3, Shot 4 |
| `ember_reel.mp4` *(optional)* | The assembled ~10s reel | Step 4–5 |

Then reference them from the docs like:

```markdown
![Ember & Comb master frame](assets/examples/ember_master_frame.png)
```

## Adding a before/after

A "generic AI default → art-directed" pair is the single most persuasive image for this toolset. If you make one, save it as `assets/examples/before_after_<brand>.png` and link it from the README.
