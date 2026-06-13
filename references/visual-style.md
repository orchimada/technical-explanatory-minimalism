# Visual Style — The Technical Reference Plate

The skill's **house style** (rule 8). Every figure is presented as a *plate*: a framed,
corner-bracketed, captioned schematic sitting on faint graph paper, labelled in
monospace like a datasheet. Distilled from the reference teardown (`teardown.html`).

This file is the single source of truth for tokens, type, the plate frame, the SVG
class system, the callout pattern, and motion. When `svg-illustration.md`,
`interactive-figures.md`, or `web-design-system.md` and this file disagree, **this wins**.

> Feel: an engineering teardown / patent plate. Warm paper, ink linework, two accents
> only, monospace chrome, "not to scale". Calm and exact, never decorative.

## Tokens (copy verbatim)

```css
:root{
  --paper:#faf9f5;   /* warm paper page background        */
  --ink:#1a1a1a;     /* linework, headings, label text    */
  --sub:#55554f;     /* secondary prose / caption text    */
  --faint:#8a8a82;   /* sub-labels, leaders, caught marks  */
  --line:#e3e2da;    /* hairlines, light tracks, dividers  */
  --red:#d23f2e;     /* accent A — the survivor / the point */
  --blue:#2553c4;    /* accent B — flow / compounding token */
  --mono:'JetBrains Mono', ui-monospace, monospace;
  --sans:'Inter', -apple-system, system-ui, sans-serif;
}
```

**Two accents, no more.** Red marks the thing that matters (the survivor, the thesis);
blue marks motion/compounding/flow. Everything structural is ink/sub/faint/line. Do not
introduce a rainbow semantic palette in this style — meaning comes from position, label,
and the two accents.

## Type

- **Prose / headlines / captions →** Inter. Headlines `font-weight:800; letter-spacing:-.035em`.
  A red period accent on the title (`Two Diagrams<span style="color:var(--red)">.</span>`).
- **All diagram labels and document chrome →** JetBrains Mono. Uppercase + letter-spacing
  for chrome (doc header, footer, `FIG. N`, meta).
- Load: `Inter:wght@400;500;600;700;800` + `JetBrains+Mono:wght@400;500;600`.

## Graph paper (the signature)

Two stacked grids. The **page** uses a faint ink grid; the **figure body** uses a finer,
faint *blue* grid (the blueprint cue).

```css
body{
  background:var(--paper);
  background-image:
    linear-gradient(rgba(26,26,26,.035) 1px, transparent 1px),
    linear-gradient(90deg, rgba(26,26,26,.035) 1px, transparent 1px);
  background-size:28px 28px;
}
.fig-body{
  background-image:
    linear-gradient(rgba(37,83,196,.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(37,83,196,.05) 1px, transparent 1px);
  background-size:14px 14px;
}
```

## The plate frame

A figure is wrapped in a bordered plate with **corner brackets** (L-marks at top-left and
bottom-right) and a caption block separated by an ink rule.

```css
.figure{ border:1.5px solid var(--ink); background:#fff; position:relative; margin:56px 0; }
.figure::before,.figure::after{ content:''; position:absolute; width:10px; height:10px; border:1.5px solid var(--ink); }
.figure::before{ top:-6px; left:-6px;  border-right:none; border-bottom:none; }
.figure::after { bottom:-6px; right:-6px; border-left:none;  border-top:none;  }
.fig-body{ padding:28px 24px 18px; overflow-x:auto; }   /* + blue grid above */
.fig-caption{ border-top:1.5px solid var(--ink); padding:14px 24px 16px; display:flex; gap:16px; align-items:baseline; }
.fig-no{ font-family:var(--mono); font-size:.72rem; font-weight:600; letter-spacing:.08em; color:var(--red); white-space:nowrap; } /* "FIG. 1" */
.fig-text{ font-size:.88rem; color:var(--sub); line-height:1.6; }   /* caption; <b> = ink 600 */
```

Document chrome (top + bottom of the page) sets the "technical reference" tone:

```
doc-head: mono · uppercase · .68rem · letter-spacing .08em · color var(--sub)
          e.g.  "Technical reference · Doc no. AD-CV-26 · Rev. D"
meta:     "Subject: … · Method: figure/ground separation · Not to scale"
footer:   mono · uppercase · .68rem · "· drawn with CSS + SVG · 0 frameworks"
```

## SVG class system (use these exact classes)

```css
text   { font-family:var(--mono); fill:var(--ink); }
.lbl   { font-size:11px;  font-weight:600; letter-spacing:.03em; }      /* part / gate title */
.lbl-s { font-size:9.5px; fill:var(--faint); letter-spacing:.02em; }    /* annotation lines  */
.lbl-r { fill:var(--red); }   .lbl-b{ fill:var(--blue); }
.wall  { stroke:var(--ink);   stroke-width:1.5; fill:none; }   /* primary structure */
.media { stroke:var(--ink);   stroke-width:1.4; fill:none; }   /* working surfaces (screens, teeth, hatch) */
.leader{ stroke:var(--faint); stroke-width:1;   fill:none; }   /* callout leaders */
.reject{ stroke:var(--red);   stroke-width:1.3; fill:none; }   /* the rejected / refracted path */
.caught{ fill:var(--faint); }                                  /* small grey marks: things stopped */
.ring  { fill:none; stroke:var(--line); stroke-width:9; }      /* thick light track (wheels/orbits) */
.node  { fill:#fff; stroke:var(--ink); stroke-width:1.5; }     /* labelled boxes, rx:4 */
/* dividers: a .wall line at opacity .4 */
```

Stroke hierarchy: `--ink` for everything real, exactly **two** accent strokes (`--red`,
`--blue`), `--faint` for anything secondary (leaders, caught marks, sub-labels). Rounded
joins/caps. Same weights across every plate in a set.

## The callout pattern (annotate like a datasheet)

Parts are labelled by a **horizontal faint leader** running to a **right-margin block**:
a `.lbl` title in caps (`GATE 1 · COARSE SCREEN`) followed by 2–3 `.lbl-s` lines. Keep all
callout titles left-aligned at the same x; let leaders span the gap. Use a short
`NAME · designator` form. Glyphs carry meaning compactly: `↓ ↗ ↻ ⚰`.

```
<line class="leader" x1="<part edge>" y1="y" x2="<margin x>" y2="y"/>
<text class="lbl"   x="<margin x+6>" y="y-8">GATE 1 · COARSE SCREEN</text>
<text class="lbl-s" x="<margin x+6>" y="y+6">the spreadsheet test — catches …</text>
```

A free-standing **principle note** (a stack of `.lbl-s` lines on the left margin) explains
the mechanism's logic in the figure itself — e.g. "FLOW ↓ / pore size shrinks downward …".

## Motion — scroll-triggered, CSS-keyframe

This style animates *ambient* figures by adding a `.play` class when the plate scrolls into
view; CSS keyframes do the rest. (For *interactive* scrub/drag figures, keep the
state→render model in `interactive-figures.md` — the two coexist.)

```js
new IntersectionObserver((es)=>es.forEach(e=>{ if(e.isIntersecting) e.target.classList.add('play'); }),
  { threshold:.3 }).observe(figureEl);
```
```css
.play .token { animation: travel 8s linear infinite; }   /* tokens fall/flow through the schematic */
.play .orbit { animation: spin 7s linear infinite; }      /* wheels turn */
.play .echo  { animation: echo 3.6s ease-out infinite; }  /* compounding rings pulse outward */
@media (prefers-reduced-motion: reduce){ *{ animation:none !important; } .token{ opacity:1 !important; } }
```

Motion is functional: tokens trace the flow, wheels turn, rings show compounding. Never
ambient drift. Always honour reduced-motion (show the resting state).

## Plate checklist

- [ ] Wrapped in a `.figure` plate with corner brackets + `FIG. N` caption?
- [ ] Page on 28px ink grid; figure body on 14px blue grid?
- [ ] All diagram labels + chrome in JetBrains Mono; prose/caption in Inter?
- [ ] Only ink/sub/faint/line + the two accents (red, blue) — no extra hues?
- [ ] Parts annotated via faint leader → right-margin `.lbl`/`.lbl-s` block?
- [ ] A left-margin principle note explaining the mechanism's logic?
- [ ] "Not to scale" / doc-no / rev chrome present?
- [ ] Ambient motion gated by `.play` on scroll; reduced-motion safe?

Start from `../assets/plate.html` (the wrapper + a sample figure) and
`../assets/starter.svg` (a static figure in this style).
