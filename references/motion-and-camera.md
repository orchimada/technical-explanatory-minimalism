# Motion & Camera — Coupled Scrubs, Real 3D, Directed Views

How figures *move*: coupling several changes to one control, carrying a tiny real 3D
model so you can orbit, and giving the camera intent. This is the machinery behind
rules 12 (couple the controls) and 14 (the camera has intent). Pair with
`interactive-figures.md`.

## Stop faking 3D — carry a model and project it

Fixed isometric slabs can't rotate. Instead keep parts as **3D boxes** (center + half
extents) and a **parameterized projection** (azimuth `az`, elevation `el`). Then orbit,
explode, section, and auto-framing all fall out of one pipeline.

```js
// rotate around Y by az, then around X by el, orthographic project.
function project(p, az, el){
  const ca=Math.cos(az), sa=Math.sin(az), ce=Math.cos(el), se=Math.sin(el);
  const x1 =  p.x*ca + p.z*sa, z1 = -p.x*sa + p.z*ca;       // yaw
  const y2 =  p.y*ce - z1*se,  z2 =  p.y*se + z1*ce;         // pitch
  return { X:x1, Y:-y2, depth:z2 };          // screen XY (+ painter depth)
}
```

Solidity at any angle comes from two cheap steps:
- **Back-face cull** — a face is visible iff its *rotated normal* points at the camera
  (`project(normal).depth > 0`). Robust at every orbit angle.
- **Painter's sort** — collect all visible faces from all parts, sort by average
  `depth`, draw far→near. This also gives correct occlusion *between* parts.
- **Light from above-front** — shade each face by `normal · light` (in world space, so
  the top face stays bright as you orbit). Map to fill-opacity over the paper.

This is ~40 lines and gives true orbitable exploded views in plain SVG — no WebGL.

## Couple the controls (rule 12)

One scrub should drive *all* the changes that belong together. The reader gets a single
legible handle; you choreograph the rest.

```js
const t = state.scrub;                 // 0..1, the one control
const az      = state.azManual + t*ORBIT;   // orbit opens up as it explodes
const spread  = t * MAX_SPREAD;             // parts separate
const shellXray = t > 0.15;                 // enclosure turns translucent to reveal
```

Keep a **manual override** alongside the coupling (drag to orbit adds to `azManual`) so
the reader still has agency — choreographed by default, explorable on demand.

## The camera has intent (rule 14)

Don't dump the reader at a default angle and make them find the view. Each state has a
*most informative* angle; move there.

- **Auto-frame per state.** Define a target `{az, el}` per step/selection (the angle that
  best reveals what just changed) and ease the camera toward it.
- **Orbit-to-reveal.** When a compartment opens, rotate so the opening faces the reader
  and the parent shell stops occluding it.
- **Ease, don't cut.** Tween camera moves (~200–400ms, ease-out). Respect
  `prefers-reduced-motion`: jump to the framed angle instead of animating.

```js
function frameTo(target){ state.camTarget = target; }      // render eases az/el → target
```

## Section-plane sweep (a cutaway you can move)

A draggable cutting plane that sweeps through the model, redrawing the cross-section as it
moves — like a CT scan. Clip faces to the plane and hatch the cut. One slider = the plane
position; far more revealing than a single fixed cutaway, and it reuses the same projection.

## Motion discipline

- Motion is **functional only** — it reveals structure or change. No ambient drift, no
  decorative spin.
- **Deterministic:** scrubbing to `t` looks identical whether dragged or auto-played.
- **One idea per move:** if a transition changes three unrelated things, split it.
- **Performance:** rebuild only the projected polygons each frame; cap to the visible
  LOD tier; pause the loop offscreen (`IntersectionObserver`).

## Checklist

- [ ] Parts are 3D boxes projected through one `project(az, el)`? (rule 11)
- [ ] Back-face cull + global painter sort → solid at every orbit angle?
- [ ] One scrub drives explode + orbit + reveal together, with manual override? (rule 12)
- [ ] Camera eases to a defined best-angle per state; reduced-motion jumps instead? (rule 14)
- [ ] Motion is functional, deterministic, one-idea-per-move?
