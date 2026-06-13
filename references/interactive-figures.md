# Interactive Figures — Explorable Explanations

How to build figures the reader *manipulates* (à la ciechanow.ski / mechanical-pencil),
not just looks at. This is the skill's **default** medium for explaining a mechanism.
Pair with the 10 rules in `../SKILL.md` and the static-drawing conventions in
`svg-illustration.md` (the stroke system, semantic palette, and annotation patterns
all still apply — interaction is layered on top).

## Choosing a substrate

- **Inline SVG + vanilla JS** — DEFAULT. Vector mechanisms, gears, schematics, exploded
  views. Themeable via CSS variables, crisp at any zoom, easy to label with real text.
- **Canvas 2D** — only when you have many elements (particles, fields, hundreds of points)
  where per-element DOM is too heavy.
- **WebGL / three.js** — only when genuine 3D (free rotation of a solid) is essential.
  Expensive to author; justify it before reaching for it.

Default to the lightest substrate that tells the story. One self-contained `.html` file
per figure (inline `<style>` + `<script>`, no build step) so it stays copy-pasteable.

## The state → render model (make scrubbing == playing)

Keep one plain `state` object and one pure `render(state)` that writes transforms/attrs.
Every interaction *mutates state*; the loop and the slider both call the same `render`.
This is what makes a figure feel solid: dragging, scrubbing, and autoplay all drive the
same single source of truth.

```js
const state = { t: 0, playing: false, speed: 1 };
function render() { /* set transforms from state — no logic, just projection */ }
function tick(now) {
  if (state.playing) { state.t += state.speed * dt; render(); }
  requestAnimationFrame(tick);
}
```

## Interaction vocabulary

- **Play / pause + rAF loop** — for continuous mechanisms. Always pair with a way to
  scrub manually.
- **Drag-to-scrub / drag-to-rotate** — pointer events on the figure; map drag delta to
  the driving parameter (angle, time). Use `setPointerCapture`; support touch.
- **Slider-scrub** — a `<input type=range>` bound to a parameter (time, explode amount).
  The most legible control for "show me the in-between states."
- **Layer toggles** — X-ray / normal, show/hide pitch circles, exploded on/off. Each
  toggle reveals hidden structure (rule 3); change one thing at a time (rule 9).
- **Hover/tap to reveal labels** — highlight a part and surface its in-place label.
  Never hide essential info behind hover alone — also respond to tap/click/focus.

## Quiet chrome for controls (rule 6)

Controls must not compete with the figure. Place them *below* it, small and `--muted`:
hairline range tracks, a single text button, monospace readouts for live values
(`ratio 1.50 : 1`, `t = 0.42 s`). No drop shadows, no gradients, no chrome that isn't
signal. The figure is loud; the controls whisper.

## Page layout — interleave prose and figures

Single readable column. Short prose sets up the next figure and points at what to
notice, then the figure, then the next idea. Decompose: isolate each part in its own
small figure before the combined one (rule 1). Optionally make the figure sticky while
related prose scrolls past it.

## Presentation & two ways to animate

Figures are presented in the house **plate** (frame + graph paper + `FIG. N` caption +
mono callouts) — see `visual-style.md` and copy `../assets/plate.html`. Labels use the
mono `.lbl` / `.lbl-s` classes; structure uses `.wall` / `.media` / `.leader`.

There are two motion patterns; pick by what the figure is for:

- **Scroll-triggered, CSS-keyframe (ambient).** For figures that *play on their own* to
  illustrate a flow — tokens travelling a path, a wheel turning, compounding rings. An
  `IntersectionObserver` adds `.play` when the plate scrolls into view; CSS keyframes do
  the rest. Lightest weight, no JS state. (This is the teardown pattern.)
- **state→render loop (interactive).** For figures the reader *drives* — drag, scrub,
  step, toggle. Keep the single `state` object + `render()` from above.

Both honour `prefers-reduced-motion` (ambient figures show their resting state with tokens
at `opacity:1`; interactive figures simply don't autoplay).

## Robustness checklist

- [ ] **`prefers-reduced-motion`** — don't autoplay; let the user scrub instead.
- [ ] **Pause when offscreen** — `IntersectionObserver` to stop the rAF work.
- [ ] **Keyboard + focus** — sliders/toggles reachable; `aria-label` on controls.
- [ ] **Touch** — pointer events, not mouse-only; `touch-action: none` on the drag surface.
- [ ] **Deterministic** — scrubbing to time T looks identical whether you dragged or played there.
- [ ] **Dark/light parity** — colors are CSS variables; figure reads in both.
- [ ] **Self-contained** — one file, no network deps, no build.

## Gold-standard examples (copy from these)

- `../assets/examples/gear-train.html` — continuous animation: meshing gears, play/pause,
  speed, **drag-to-scrub**, live ratio readout, color-identity labels, pitch-circle toggle.
- `../assets/examples/layered-reveal.html` — progressive disclosure: **exploded-view
  slider** + **X-ray toggle** + tap-to-highlight, dashed reassembly leaders.

Both demonstrate the state→render model, quiet chrome, reduced-motion handling, and the
shared palette/stroke system. Start a new figure by copying the closest one.
