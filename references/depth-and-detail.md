# Depth & Detail — Inner Compartments, Nesting, Level-of-Detail

How to handle fine internal detail and parts-within-parts *without* clutter. This is
where a figure stops being a flat picture and becomes a navigable model (rule 13).
Pair with `interactive-figures.md` and `motion-and-camera.md`.

## The core idea: depth is navigable, not drawn-all-at-once

A bespoke author draws every screw because they only draw one frame. We model the
hierarchy and **reveal detail on demand**. Two mechanisms do the work:

1. **Recursive part grammar** — a part *contains* parts, drawn with the same
   conventions (stroke system, color identity, labels). Opening a part shows its
   internal figure. There is no special "detail mode" — it's figures all the way down.
2. **Level-of-detail (LOD)** — each detail tier has a visibility condition. Show coarse
   structure when zoomed out / collapsed; reveal fine structure only when it is large
   enough on screen to read. Detail that can't be read is noise — cull it.

```
// every part carries its detail tier and a visibility predicate
{ id:'chip', tier:2, visibleWhen: s => s.open.board || s.zoom > 1.6, ... }
// render skips tiers whose predicate is false → no clutter, no wasted ink
```

## Modelling nested compartments

- Model parts in a **tree**: `device → board → {chip, connector, mounts}`. Each node has
  its own local origin; children are positioned relative to the parent.
- **Open = local explode.** Opening a compartment runs the same explode transform on its
  children that the top level uses on its parts (rule 11/12 reuse). Closing reseats them.
- **Inherit identity, vary value.** A child keeps the parent's hue family but shifts
  value/saturation so it reads as "inside the board," not a new top-level system.
- **Occlusion is a feature.** When a compartment opens, make the enclosing shell
  translucent or sectioned so you see *into* it — don't move the shell away and lose the
  spatial relationship. Reveal-in-place beats reveal-by-removal.

## Fine-detail conventions (borrowed from engineering drawing)

- **Detail callout (magnified inset).** Circle the small region, draw a leader to a larger
  circle elsewhere that shows it magnified — label the scale (`DETAIL A — 4×`). This is the
  canonical way to show something too small to read in context. Underused on the web; use it.
- **Section hatching.** Cut surfaces get thin 45° hatching (`--stroke-detail`); different
  materials get different hatch spacing/angle. Signals "this is solid, you're seeing a cut."
- **Fasteners & repeated features:** draw one in full, ghost the rest (centerline + hole)
  with a `4×` note. Don't lovingly render 16 identical screws.
- **Centerlines** (long-dash-dot) for axes of symmetry and rotation — orients the reader
  and marks where things spin or align.
- **Break lines** to truncate long uniform runs (a long shaft) so the figure stays compact.

## LOD as the antidote to clutter

The failure mode of "more detail" is a busy, unreadable figure. Discipline:

- **One tier visible at rest.** The collapsed figure shows only top-level parts + their
  labels. Everything finer is behind a zoom/open gate.
- **Detail enters as you commit attention.** Open a compartment or zoom past a threshold →
  the next tier fades in *and* its labels appear; the tier above can dim or simplify.
- **Labels obey the same gate.** A part's label is drawn only when the part is. Never label
  something the reader can't currently see.
- **Budget the ink.** If a tier would add more than ~7 new labels at once, it's two tiers.

## Checklist

- [ ] Parts modelled as a tree; children positioned in the parent's local frame? (rule 11)
- [ ] Each detail tier has a visibility predicate; only one tier shows at rest? (rule 13)
- [ ] Opening a compartment reveals *in place* (shell goes translucent/sectioned)?
- [ ] Too-small detail handled by a magnified callout, not by cramming?
- [ ] Repeated features ghosted with a count, not drawn N times?
- [ ] Labels gated to their tier — nothing labelled that isn't visible?
