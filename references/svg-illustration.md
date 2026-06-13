# SVG Illustration — How to Build the Figures

How to produce diagrams in the technical-explanatory minimalist style. Pair with
the 10 rules in `../SKILL.md` and the philosophy in `design-principles.md`.

## Why SVG

Scalable line-art, themeable via CSS variables (dark/light parity for free),
annotatable with real text, and it reads like a datasheet. Default to SVG for any
static diagram; reach for HTML+CSS/JS only when the figure must be interactive.

## The stroke system

One coherent house style means a fixed, small set of stroke weights:

- `--stroke-structural: 2`  — main outlines / part boundaries.
- `--stroke-detail: 1`      — internal detail, hatching.
- `--stroke-leader: 1`      — callout leader lines (often dashed).
- Rounded line joins/caps (`stroke-linejoin="round" stroke-linecap="round"`) for a
  calm, physical feel. Keep weights consistent across every figure in a set.

## Semantic palette (color = identity)

Define colors once as CSS variables and reuse them so a part keeps its hue
everywhere. Reserve saturated color for *meaning*; everything structural stays neutral.

```
:root {
  --paper:  #f5f3ee;   /* near-paper background          */
  --ink:    #1d1d1f;   /* outlines, body text            */
  --muted:  #8a8a8e;   /* secondary detail, hatching     */
  /* semantic part colors — assign one per named component, keep stable */
  --part-1: #d6453d;   /* red    */
  --part-2: #e0a93b;   /* amber  */
  --part-3: #3d7dd6;   /* blue   */
  --part-4: #3aa676;   /* green  */
  --accent: #d6453d;   /* signal / CTA only              */
}
@media (prefers-color-scheme: dark) {
  :root { --paper:#121212; --ink:#ececec; --muted:#7d7d82; }
}
```

Rules: at most ~4 semantic part colors per figure; structural geometry uses
`--ink`/`--muted` only; the same component → the same `--part-N` in every figure and
in the prose that references it.

## Figure types and how to construct them

- **Flow / pipeline** — boxes left→right or top→bottom in the *causal* order of the
  real system; arrows show direction of force/data. Layout mirrors mechanism (rule 7).
- **Exploded view** — separate parts along a single axis with thin dashed alignment
  lines showing how they reassemble. Keep spacing even; preserve relative scale.
- **Cutaway** — clip the outer shell (SVG `clipPath` or a section plane) to reveal
  internals; hatch the cut surface with `--stroke-detail` lines at ~45°.
- **Annotated schematic** — neutral geometry + in-place labels; use part designators
  (`R1`, `C3`) in monospace for a datasheet feel.
- **Step sequence** — repeat the same figure N times, each adding one change; highlight
  the delta with `--accent`.

## Annotation patterns (annotate in-place — rule 5)

- Labels sit on/near the part, connected by a thin dashed leader line to a small dot
  at the anchor point. Avoid separate captions.
- Monospace for data, designators, and measurements; clean sans for descriptive labels.
- Keep label text `--ink`; never color label text with the part color — instead put a
  small color swatch/dot beside it so color stays the identity cue.

## Structural template

```
<svg viewBox="0 0 800 500" xmlns="http://www.w3.org/2000/svg"
     stroke-linejoin="round" stroke-linecap="round">
  <style>/* :root vars above; .struct{stroke:var(--ink);fill:none;stroke-width:2}
            .detail{stroke:var(--muted);stroke-width:1}
            .leader{stroke:var(--muted);stroke-width:1;stroke-dasharray:3 3}
            .label{font:13px ui-sans-serif;fill:var(--ink)}
            .desig{font:12px ui-monospace;fill:var(--ink)} */</style>
  <rect width="800" height="500" fill="var(--paper)"/>
  <!-- parts as <g> grouped & colored by identity; leaders + labels last -->
</svg>
```

See `../assets/starter.svg` for a working, themeable starting point.

## Self-check before shipping

- [ ] Each part isolated/identifiable before the whole? (rule 1)
- [ ] Same color + name for each part everywhere? (rule 2)
- [ ] Internal structure revealed where it matters? (rule 3)
- [ ] Labels on the artwork, not in a caption? (rule 5)
- [ ] Neutral background, no non-signal ornament? (rule 6)
- [ ] Layout order matches the real causal flow? (rule 7)
- [ ] Stroke weights/palette consistent with the rest of the set? (rule 8)
