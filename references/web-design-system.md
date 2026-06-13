# Minimalist Web / Interface Design System

Token system for building restrained, information-dense interfaces in the same
school as the reference sites. Pair with the 10 rules in `../SKILL.md`. The canonical
tokens, type, graph paper, and the figure *plate* live in `visual-style.md` — this file
applies them to full interfaces.

## Foundations

- **Near-paper background, ink text.** Not pure white/black — a warm off-white and a
  near-black keep the surface calm. Reserve saturated color for meaning/signal.
- **Dark/light parity from the start.** Define every token in both modes; never
  invert as an afterthought.
- **One strong reading column.** Dense content gets a single ~60–72ch measure with
  generous margins, not full-bleed text.

## Color tokens

```
:root{
  --paper:#faf9f5;  --surface:#ffffff;  --line:#e3e2da;
  --ink:#1a1a1a;    --sub:#55554f;      --faint:#8a8a82;
  --red:#d23f2e;    /* accent A — the point / primary action */
  --blue:#2553c4;   /* accent B — flow / links / compounding  */
}
@media (prefers-color-scheme: dark){
  :root{ --paper:#16150f; --surface:#1c1b16; --line:#2a2a24;
         --ink:#ececec; --sub:#b4b4ac; --faint:#7d7d76; }
}
```

**Two accents, no more** — red and blue. Keep them rare; when everything is ink/sub/faint,
an accent reads as *signal*. (This style is paper-first; the dark map above is a faithful
adaptation, not the primary.)

## Type

- **Clean sans for prose**, **monospace for data, labels, code, designators.** The
  monospace/technical-caps treatment is what signals "instrument panel."
- Restrained modular scale (e.g. 13 / 15 / 18 / 24 / 32 / 48); generous line-height
  (~1.55) for body, tight for data tables.
- Use small caps or letter-spaced uppercase for section/category labels.

```
:root{
  --sans:'Inter', -apple-system, system-ui, sans-serif;   /* prose, headlines */
  --mono:'JetBrains Mono', ui-monospace, monospace;        /* labels, data, chrome */
  --t-xs:13px; --t-sm:15px; --t-md:18px; --t-lg:24px; --t-xl:32px; --t-2xl:48px;
}
```

Headlines: Inter `800`, `letter-spacing:-.035em`, with a red period accent. Document chrome
(headers, footers, `FIG. N`, meta) is mono, uppercase, ~.68rem, `letter-spacing:.06–.08em`.

## Graph paper & plates

This style sits on faint graph paper, and framed content is a **plate** (border + corner
brackets + caption). Both are specified in `visual-style.md`:

- **Page** — 28px ink grid (`rgba(26,26,26,.035)`).
- **Figure/plate body** — 14px *blue* grid (`rgba(37,83,196,.05)`) — the blueprint cue.
- **Plate** — `1.5px` ink border, white fill, L-shaped corner brackets, an ink-ruled
  caption row with a red `FIG. N` and a sans caption. Copy `../assets/plate.html`.

## Spacing & layout

- 4/8px spacing scale; lean on the larger steps — whitespace is the primary tool.
- **Grid discipline:** regular, repeating blocks; uniform tiers/cards; align to a
  baseline. Regularity = scannability.
- Remove non-signal chrome: hairline borders (`--border`) over boxes/shadows; flat
  surfaces; minimal elevation.

## Figures & data are first-class

- Style diagrams, tables, and labels as content, not decoration. Annotate in place.
- Tables: monospace numerals, right-aligned numbers, hairline row rules, no zebra
  unless density demands it.
- Use the `--data-N` hues consistently so a series/category keeps its color everywhere.

## Motion & disclosure

- Motion is functional only — reveal structure (expand/cutaway/toggle), never ambient.
- Progressive disclosure: collapse complexity behind toggles; each interaction adds
  one idea (rule 9).

## Self-check

- [ ] Background near-paper, accent rare and meaningful? (rule 6)
- [ ] Both dark and light defined?
- [ ] One stable semantic color per data category? (rule 2)
- [ ] Monospace for data/labels, sans for prose?
- [ ] Whitespace + grid doing the work; chrome stripped?
- [ ] Figures/tables annotated in place as first-class content? (rule 5)
