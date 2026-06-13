---
name: technical-explanatory-minimalism
description: >
  Create concise, minimalist technical diagrams, schematics, and explanatory
  illustrations (SVG-first), and design clean minimalist web/interface design
  systems. Use when the user wants to explain a mechanism or system visually,
  make an exploded view / cutaway / flow diagram / annotated figure, illustrate
  how something works, or build a restrained, information-dense UI / design
  tokens in the style of ciechanow.ski, makingsoftware.com, diode.computer, or
  mechanical-pencil.com.
---

# Design — Technical-Explanatory Minimalism

A skill for two related crafts that share one aesthetic:

- **(A) Technical illustration** — diagrams, schematics, exploded views, cutaways,
  flow diagrams, and annotated explanatory figures.
- **(B) Minimalist design systems** — restrained, information-dense web/interface
  systems (tokens, type, layout, color-as-meaning).

Both follow the same school: **illustration-led explanation, quiet chrome, color as
identity, decompose-then-compose.** Full philosophy and the reference-site analysis
live in `references/design-principles.md` — read it when you need the *why*.

## The 10 rules (apply to every output)

1. **Decompose, then compose.** Show each part in isolation before combining.
   Never lead with the finished whole.
2. **Color/label = stable identity.** A part keeps the same hue and name in every
   figure and in the prose. Color carries meaning, never decoration.
3. **Reveal the hidden.** Use cutaways, exploded views, and X-ray/normal toggles to
   expose internal structure.
4. **Diagram leads, text glues.** The figure carries the explanation; prose only
   frames it and points at what to notice.
5. **Annotate in-place.** Labels and callouts live on the artwork, not in a separate caption.
6. **Quiet chrome, loud content.** Neutral near-paper background, generous whitespace,
   no ornament. All visual energy goes to the figure/content.
7. **Spatial = causal.** Layout order mirrors how the real system flows or works.
8. **One coherent house style.** The house style is the **technical reference plate** —
   framed, corner-bracketed, captioned schematics on faint graph paper, labelled in
   monospace, with a strict two-accent (red/blue) palette. It is specified in full in
   `references/visual-style.md`; follow it for every figure.
9. **Progressive disclosure.** Reveal complexity on demand; each step adds one idea.
10. **Curiosity as the entry point.** Start from a felt question; exhaust one thing well.

## Beyond the references — what makes a figure *ours*

The reference sites are hand-authored masterpieces; out-artisaning them frame-by-frame
is a losing game and reads as imitation. Our edge is treating a figure as a **model that
yields many views**, not a drawing. Apply these *on top of* the 10 fidelity rules:

11. **Model, don't draw.** Encode the thing as data — parts, nesting, states, relations —
    and render from it. It then regenerates under new parameters or live data and stays
    consistent. (See `references/motion-and-camera.md`.)
12. **Couple the controls.** One scrub drives many coordinated changes (explode + orbit +
    transparency + section). Author choreographs; reader gets one legible handle — keep a
    manual override for agency.
13. **Depth is navigable.** Compartments open into their own figures with the same grammar;
    level-of-detail reveals fine structure only when it's legible. (See
    `references/depth-and-detail.md`.)
14. **The camera has intent.** Auto-frame/orbit to the most informative angle per state
    instead of leaving the reader to hunt for the view.
15. **Be data-honest.** Put real magnitudes, tolerances, ranges, and units on the figure —
    idealized geometry annotated with the messy truth.
16. **Linked multi-view.** Brush the same part across schematic + section + exploded at once.
17. **Mechanism = state machine.** Model states + transitions; let the figure *prove* the
    logic, not just animate it.

When a request would otherwise just reproduce a reference, reach for these — they are
where the skill stops imitating and starts compounding.

## Workflow

### A — Making a technical diagram / illustration

1. **Clarify the subject and the one thing to explain.** Ask only if genuinely
   ambiguous; otherwise pick the obvious framing and state it.
2. **Decompose** the system into named parts. Assign each a stable color from the
   semantic palette (`references/svg-illustration.md`).
3. **Choose the figure type**: flow/pipeline, exploded view, cutaway, annotated
   schematic, or step sequence. Match spatial layout to causality (rule 7).
4. **Decide static vs. interactive.** If the thing *moves* or has hidden states the
   reader should explore, build an **interactive figure** (the default for mechanisms)
   — copy the closest example in `assets/examples/` and follow
   `references/interactive-figures.md`. If it's a fixed schematic, copy
   `assets/starter.svg`. Either way, present it in the **plate** and follow the house
   style in `references/visual-style.md` — the class system, two-accent palette, and
   right-margin callouts are shared.
5. **Annotate in place** — labels on the artwork, leader lines to parts.
6. **Self-check against the 10 rules** (and the interactive checklist if applicable),
   then render to the user — write the `.html`/`.svg` file (it appears in the preview
   panel) or use the visualize tools for a quick inline look.

### B — Designing a minimalist web/interface system

1. **Read `references/web-design-system.md`** for the token system.
2. **Establish the foundation**: near-paper background, ink text, one small semantic
   palette, restrained type scale, generous spacing, dark/light parity from the start.
3. **Apply grid discipline** — regular, scannable blocks; remove non-signal chrome.
4. **Make figures/data first-class** — diagrams, tables, and labels styled as content,
   annotated in place, with monospace for data and technical labels.
5. **Verify** by rendering and checking against rules 6, 7, 8.

## Output formats

Every figure is presented as a **plate** in the house style (`references/visual-style.md`):
framed + corner-bracketed + `FIG. N` caption, on graph paper, monospace callouts, two
accents. Start from `assets/plate.html` (wrapper + sample) and `assets/starter.svg`.

- **Interactive HTML + JS** is the default for *mechanisms* — explorable figures the
  reader drags, scrubs, and toggles (the ciechanow.ski model). One self-contained file,
  inline SVG + vanilla JS, no build. See `references/interactive-figures.md`.
- **Static SVG inside a plate** for fixed schematics — scalable, monospace-labelled,
  annotated via right-margin callouts; prints like a datasheet.
- **HTML + CSS** for design-system demos.
- Files written to `assets/` (or the user's project) appear in the preview panel; use
  the `visualize` tools for a quick inline look.

## Reference files

- `references/visual-style.md` — **the house style**: tokens, type, graph paper, the plate
  frame, the SVG class system, callouts, motion. Canonical for all presentation.
- `references/design-principles.md` — philosophy + per-site analysis (the *why*).
- `references/interactive-figures.md` — explorable-explanation patterns: state→render
  model, drag/scrub/toggle vocabulary, quiet-chrome controls (the *how* for mechanisms).
- `references/depth-and-detail.md` — inner compartments, nested parts, level-of-detail,
  engineering detail callouts (the *how* for rules 13).
- `references/motion-and-camera.md` — real 3D from a parameterized projection, coupled
  scrubs, orbit-on-explode, section sweeps, directed camera (the *how* for rules 11/12/14).
- `references/state-machines.md` — model a mechanism as states+transitions and prove its
  logic with a linked state diagram (the *how* for rules 16/17).
- `references/svg-illustration.md` — static-figure craft: stroke system, semantic
  palette, exploded/cutaway/callout techniques (shared by interactive figures too).
- `references/web-design-system.md` — minimalist UI tokens: palette, type, spacing,
  dark/light parity (the *how* for interfaces).
- `assets/plate.html` — the canonical figure **plate** wrapper (frame, graph paper, caption,
  chrome, scroll-triggered motion) + a sample figure. Copy this to start any new figure.
- `assets/starter.svg` — a static figure in the house style (mono labels, callout, accents).
- `assets/examples/gear-train.html` — gold-standard interactive figure (animation + drag-scrub).
- `assets/examples/layered-reveal.html` — gold-standard interactive figure (explode + X-ray).
- `assets/examples/orbit-explode.html` — gold-standard: real-3D coupled explode + orbit +
  openable nested compartment with LOD (rules 11–14 in one figure).
- `assets/examples/state-machine.html` — gold-standard: click-pen mechanism modelled as a
  state machine with a linked, highlighting state diagram (rules 16/17).
