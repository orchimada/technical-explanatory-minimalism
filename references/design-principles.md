# Technical-Explanatory Minimalism — Reference Design Principles

Distilled from four reference sites that share a recognizable school of design:
illustration-led technical explanation and concise, minimalist information design.

Sources:
- Ciechanowski — *Mechanical Watch* — https://ciechanow.ski/mechanical-watch/
- Diode Computers — https://www.diode.computer/
- Making Software (Dan Hollick) — https://www.makingsoftware.com/
- Mechanical Pencil — *Pen breakdown* — https://mechanical-pencil.com/products/pen

---

## 1. Ciechanowski — *Mechanical Watch*

The gold standard for "explorable explanations."

- **Build one part at a time, then compose.** Each concept gets its own isolated
  figure before parts combine into the full mechanism (spring → barrel → gear
  train → escapement → balance wheel). Never shows the whole system first.
- **Color as a naming system.** Each component has a fixed, consistent hue used in
  *every* diagram and referenced in the prose. Color = identity, not decoration.
- **Interactive over static.** Draggable 3D / scrubbable WebGL figures. The reader
  manipulates the mechanism (rotate, slider-scrub time, toggle layers).
- **Diagram-first, prose-as-glue.** Illustrations carry the explanation; text sets
  up the next figure and points at what to notice. Tight interleaving.
- **Minimal, neutral chrome.** Cream/off-white background, sans-serif body, generous
  whitespace, no ornamentation. All visual energy goes to the diagrams. Single column.
- **Spatial layout mirrors causality.** Energy-flow arranged in the same order the
  real mechanism transmits force.
- **Honest physical rendering.** Soft real-world lighting/shadow, accurate proportions.

## 2. Diode Computers

A product site that uses schematic vocabulary as its aesthetic.

- **The schematic IS the brand.** PCB line-art, part designators (`PI0004`, `EL002`,
  `AM0001`), engineering naming conventions as visual identity. Reads like a datasheet.
- **"X-ray" / dual-view pattern.** Each board shown "Normal" and "X-ray" — surface vs.
  internal structure. Reveals hidden layers deliberately.
- **Dark/light parity.** Every asset has dark and light variants, designed from the start.
- **Monospace / technical-caps typography** for labels and designators; clean bold sans
  for headlines. Type signals "instrument panel."
- **Strict, scannable blocks.** High regularity, grid discipline, uniform tiers.
- **Restrained palette.** Neutral black/white/gray base, sparing accent reserved for signal/CTA.

## 3. Making Software (Dan Hollick)

Illustrated reference manual for how software works (anti-aliasing, blur, color, touchscreens).

- **"Have you ever wondered…" framing.** Each chapter starts from everyday curiosity,
  then dissects the mechanism. Curiosity-driven, not API-driven.
- **Diagrams do the heavy lifting.** Explicit principle: pictures and diagrams carry
  the load; text is deliberately lightweight.
- **Bespoke, consistent illustration language.** Flat clean vector diagrams, unified
  stroke weight, limited palette, recurring motifs — a coherent house style.
- **Annotated figures.** Labels, callouts, step sequences directly on the artwork.
- **Reference-manual structure.** Modular, self-contained chapters; built for lookup.
- **Progressive disclosure.** Concepts decompose simple → complex; each diagram adds one idea.

## 4. Mechanical Pencil — *Pen breakdown*

Ciechanowski's approach applied to everyday objects.

- **Narrative scroll with a mechanical reveal.** Question-led headings pace the story.
- **Exploded views + cutaways as the core device.** Parts separated along an axis to
  show assembly, then sectioned to show internal motion. 2D and 3D of the same part.
- **Interactive over photographic.** Illustrated/animated, not photographed — hide
  irrelevant detail, emphasize the mechanism; the reader can actuate it.
- **Conversational, first-person copy.** Disarming, low-jargon, paired with rigorous detail.
- **One object, fully understood.** Tight scope — exhaust a single artifact completely.

---

## Cross-cutting principles (the shared design language)

| Principle | In practice |
|---|---|
| **Decompose, then compose** | Isolate each part in its own figure; combine only after each is understood. |
| **Color/label = stable identity** | A part keeps the same color and name across every diagram and in prose. |
| **Reveal the hidden** | Cutaways, exploded views, X-ray/normal toggles — make internal structure visible. |
| **Show, let them touch** | Interactive manipulation (drag, scrub, actuate) beats static captions. |
| **Diagram leads, text glues** | Visuals carry the explanation; prose only frames and points. |
| **Annotate in-place** | Labels and callouts live on the artwork, not in separate captions. |
| **Quiet chrome, loud content** | Neutral background, generous whitespace, minimal UI. |
| **Spatial = causal** | Layout order mirrors how the real system flows/works. |
| **One coherent house style** | Unified stroke weight, palette, and lighting model across all figures. |
| **Curiosity as the entry point** | Start from a felt question, decompose progressively, exhaust one thing well. |

---

## Translating to a minimalist web/interface design system

- **Neutral, near-paper background; ink-like text.** Reserve saturated color for meaning.
- **A small, fixed semantic palette** where each hue carries a stable meaning across the UI.
- **Generous whitespace and a single strong reading column** for dense content.
- **Monospace/technical type for labels and data**, clean sans for prose, restrained scale.
- **Diagrams and figures as first-class content**, not decoration — annotated in place.
- **Progressive disclosure**: reveal complexity on demand (toggles, cutaways, expand).
- **Grid discipline and regularity** for scannability; remove all non-signal chrome.
