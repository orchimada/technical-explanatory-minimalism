# Design — Technical-Explanatory Minimalism

A [Claude](https://claude.com/claude-code) **skill** for making concise, minimalist
technical diagrams and explorable explanations — and for designing the kind of quiet,
information-dense interfaces they live in.

It distills a recognizable school of design — illustration-led technical explanation —
from four reference sites, turns it into explicit rules, and backs those rules with
working, verified gold-standard examples.

> The goal isn't to *imitate* hand-crafted explainers like ciechanow.ski. It's to treat
> a figure as a **model that yields many views** — parametric, navigable, data-driven,
> and provable — which is the thing a bespoke author can't easily do.

---

## What it does

Two related crafts, one aesthetic:

- **(A) Technical illustration** — diagrams, schematics, exploded views, cutaways, flow
  diagrams, and interactive *explorable* figures you drag, scrub, and step through.
- **(B) Minimalist design systems** — restrained, information-dense web/interface systems
  (tokens, type, layout, color-as-meaning) with dark/light parity.

Interactive figures are built as **one self-contained `.html` file** — inline SVG + vanilla
JS, no build step, themeable via CSS variables.

## The principles

The skill is organized around two tiers of rules (full text in [`SKILL.md`](SKILL.md)):

**Fidelity (1–10)** — make it look right: decompose-then-compose · color = stable identity ·
reveal the hidden · diagram leads, text glues · annotate in place · quiet chrome, loud
content · spatial = causal · one house style · progressive disclosure · curiosity as the
entry point.

**Beyond the references (11–17)** — make it *ours*: model don't draw · couple the controls ·
depth is navigable · the camera has intent · be data-honest · linked multi-view ·
mechanism = state machine.

## Gallery — gold-standard examples

Self-contained, verified in light **and** dark mode. Open any file in a browser, or serve
the folder and visit it.

| Example | Demonstrates |
|---|---|
| [`four-stroke-engine.html`](assets/examples/four-stroke-engine.html) | **Flagship.** A four-stroke engine: crank-slider mechanism + the cycle as a state machine + a live P–V (Otto) plot, all driven by one crank angle. Play / scrub / step. |
| [`orbit-explode.html`](assets/examples/orbit-explode.html) | Real 3D from a parameterized SVG projection — one scrub couples explode + orbit, with an openable nested compartment and level-of-detail. |
| [`state-machine.html`](assets/examples/state-machine.html) | A click-pen modelled as a state machine with a linked, highlighting state diagram — *proves* the logic instead of animating it. |
| [`layered-reveal.html`](assets/examples/layered-reveal.html) | Exploded view + X-ray toggle + tap-to-isolate, with labels that travel with their part. |
| [`gear-train.html`](assets/examples/gear-train.html) | Continuous mechanism: meshing gears, play/pause, drag-to-scrub, live ratio readout. |

A static line-art starting point lives in [`assets/starter.svg`](assets/starter.svg).

## Repository layout

```
.
├── SKILL.md                     # entry point: rules 1–17 + A/B workflows
├── references/                  # the "how" — load on demand
│   ├── design-principles.md     #   philosophy + per-site analysis
│   ├── interactive-figures.md   #   state→render, drag/scrub/toggle, quiet chrome
│   ├── depth-and-detail.md      #   inner compartments, nesting, level-of-detail
│   ├── motion-and-camera.md     #   real 3D projection, coupled scrubs, directed camera
│   ├── state-machines.md        #   model & prove a mechanism's logic
│   ├── svg-illustration.md      #   static-figure craft (stroke system, palette, callouts)
│   └── web-design-system.md     #   minimalist UI tokens + dark/light parity
└── assets/
    ├── starter.svg              # themeable static template
    └── examples/                # the gold-standard interactive figures
```

## Using it as a Claude skill

Drop this directory where your Claude skills live (e.g. a `skills/` folder for a plugin, or
`~/.claude/skills/design/`). Claude reads [`SKILL.md`](SKILL.md)'s frontmatter to decide when
to invoke it, then pulls in `references/` as the task needs them and copies from
`assets/examples/` as starting points.

You can also just read it as a design handbook — the rules and references stand on their own.

## Previewing the examples

Any example is a plain file — open it directly, or serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/assets/examples/four-stroke-engine.html
```

## Credits

The design language is distilled from these references, with gratitude:

- [Bartosz Ciechanowski — *Mechanical Watch*](https://ciechanow.ski/mechanical-watch/)
- [Diode Computers](https://www.diode.computer/)
- [Dan Hollick — *Making Software*](https://www.makingsoftware.com/)
- [Mechanical Pencil](https://mechanical-pencil.com/products/pen)
