# Naming Engine — STATE

R&D toward an **AI naming *strategist*** — a tool that helps you understand *why* a great name works and arrive at one with conviction, not a name generator that hands you a list. This repo holds the **interactive interaction-design prototypes**. (Strategy, competitive analysis, and the lens/evaluation methodology are kept private, outside this repo.)

> **Live:** https://nessim-higson.github.io/naming-engine/

---

## The direction

A name shouldn't be *filled into a form* — it should **surface from your idea**. So the interface is an emergent **type-field you fly through**, inspired by the [Kunumi](https://github.com/nessim-higson) latent-starfield mechanic (things absent at rest → materialize as you go deeper) but reskinned to **type, not images** (a naming engine's content is *language*).

The experience, end to end:
1. **Type your idea** (ramble — no questionnaire). Your words **surface** as type nodes in space.
2. **Pause** → the engine *reflects a brief back*: it resolves your feeling/positioning, threaded to the words that implied it (provenance made visible — it shows its work).
3. **Advance** → the camera **flies forward in Z** through the cloud, past your words and the lens territories, toward the names.
4. **Names bloom** from the field, each tagged with the **lens** that produced it.
5. **Tap a name** → a verdict sheet: an evaluation score, the origin story, and a "Connected · same world" strip — its *why*.

A **depth nav rail** (Idea · Feeling · Lenses · Names) lets you travel between stages = fly through the cloud.

---

## Prototypes (the journey)

Each is a single self-contained `index.html`. Listed oldest → newest; **`mockup-zspace` is the current canonical direction.**

| Prototype | What it explores | Status |
|---|---|---|
| [`mockup-orientation`](mockup-orientation/) | First pass: a stepped onboarding wizard + live "lens" reactivity, 3 reskinnable themes | superseded (felt like a form) |
| [`mockup-seed`](mockup-seed/) | "Brief as a living artifact" — a generative flow-field that recolors by feeling, crystallizes on commit | direction probe |
| [`mockup-listen`](mockup-listen/) | "Listen, don't ask" — dump a ramble → engine extracts + reflects the brief back | input-model probe |
| [`mockup-typefield`](mockup-typefield/) | Type nodes that **surface as you type** and resolve into a threaded brief | mechanic probe |
| [`mockup-emergence`](mockup-emergence/) | Full flat loop: type → brief → **names bloom from the field** → tap for verdict | full-loop, flat |
| **[`mockup-zspace`](mockup-zspace/)** | **The flat field given real Z-depth — a volumetric word-cloud you fly through, with a depth nav rail** | **canonical** |

---

## Architecture

- **Self-contained, no build step.** Each prototype is one HTML file: inline CSS + vanilla JS, Canvas 2D. Fonts via Google Fonts (Fraunces / Inter / Space Mono).
- **3D via perspective projection in Canvas 2D** (same technique as the Kunumi starfield): each node has world `(x, y, z)`; a camera at `camZ` flies forward; project `sx = W/2 + x · FOCAL/(z−camZ)`, size & opacity scale with depth. No WebGL/Three.js needed → fast and light.
- **Wet-cement theming.** All color/type/spacing are CSS custom properties; the generative palettes are data objects keyed by "feeling." Reskin = change tokens, not structure.
- **Mobile-first.** Every prototype is built to work at ~380px: full-width input island, verdict as a **bottom sheet** (vs. a side card on desktop), the depth rail reflows to a horizontal stage row. `viewport-fit=cover` + safe-area insets.

---

## Honest current state

- **The intelligence is mocked.** Brief extraction is a keyword heuristic; name candidates come from a small per-feeling bank. The real version is a single LLM call that generates names from the *full* brief × the relevant lenses — and will be much stronger (and work on *any* idea, not just the bundled example).
- **Known rough edges:** on small screens, bloomed names can crowd the center brief label; the lens labels in Z are placed semi-randomly (could be deliberately composed); motion through Z is functional but not yet cinematic.
- `mockup-zspace` leaves a `window.__z()` debug hook for inspecting camera state.

---

## Next

1. **Wire real intelligence** — live LLM extraction + name generation, so it works on a real idea you type. (Turns the demo into a tool.)
2. **Cinematic pass** — easing/motion-blur on the flythrough, a settle on arrival, deliberate lens composition, sound.
3. **Polish mobile** — fix center-crowding, tune the depth rail.

---

## Run locally

Any static server from the repo root, e.g.:

```bash
python3 -m http.server 8080
# then open http://localhost:8080/mockup-zspace/
```
