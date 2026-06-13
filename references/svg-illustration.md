# SVG Illustration — How to Build the Figures

How to produce diagrams in the technical-explanatory minimalist style. Pair with
the 10 rules in `../SKILL.md` and the philosophy in `design-principles.md`.

> **Presentation is governed by `visual-style.md`** (the house style) — tokens, type,
> the plate frame, the SVG class names (`.wall`/`.media`/`.leader`/`.reject`/`.caught`,
> `.lbl`/`.lbl-s`), the two-accent palette, the right-margin callout, and motion. This
> file covers figure *construction* (figure types, exploded/cutaway/callout geometry).
> Where they differ, `visual-style.md` wins. Finished figures sit inside `../assets/plate.html`.

## Why SVG

Scalable line-art, themeable via CSS variables (dark/light parity for free),
annotatable with real text, and it reads like a datasheet. Default to SVG for any
static diagram; reach for HTML+CSS/JS only when the figure must be interactive.

## The stroke system (house classes)

Use the named classes from `visual-style.md` — a fixed, small set:

- `.wall`   — ink, 1.5 — primary structure / part boundaries.
- `.media`  — ink, 1.4 — working surfaces (screens, teeth, hatch, prisms).
- `.leader` — faint, 1 — callout leader lines.
- `.reject` — red, 1.3 — the rejected / refracted / "out" path.
- dividers  — a `.wall` line at `opacity:.4`.
- `.caught` — faint fill — small marks for things stopped/filtered.
- Rounded joins/caps for a calm, physical feel. Same weights across every plate in a set.

## Palette

Use the house tokens from `visual-style.md`. The default is **two accents only** — red
for the thing that matters, blue for flow/compounding — over ink/sub/faint/line structure.

```
:root{
  --paper:#faf9f5; --ink:#1a1a1a; --sub:#55554f; --faint:#8a8a82; --line:#e3e2da;
  --red:#d23f2e;   /* the survivor / the point */
  --blue:#2553c4;  /* flow / motion / compounding */
}
```

**Most schematics need no more than this** — meaning comes from position, label, and the
two accents, not from a rainbow.

**Exception — multi-part assemblies** (exploded views, the engine cross-section): when a
figure must distinguish many real parts at once, color *is* identity and a small extra
palette is justified. Keep it harmonized with the house tokens, assign one stable hue per
named part (used everywhere that part appears), and still draw all structure in `--ink`:

```
--part-1:#d23f2e; --part-2:#e0a93b; --part-3:#2553c4; --part-4:#3aa676;  /* ≤4, stable */
```
Reach for this only when parts genuinely need telling apart; otherwise stay two-accent.

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
