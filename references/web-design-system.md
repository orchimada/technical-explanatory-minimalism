# Minimalist Web / Interface Design System

Token system for building restrained, information-dense interfaces in the same
school as the reference sites. Pair with the 10 rules in `../SKILL.md`.

## Foundations

- **Near-paper background, ink text.** Not pure white/black — a warm off-white and a
  near-black keep the surface calm. Reserve saturated color for meaning/signal.
- **Dark/light parity from the start.** Define every token in both modes; never
  invert as an afterthought.
- **One strong reading column.** Dense content gets a single ~60–72ch measure with
  generous margins, not full-bleed text.

## Color tokens

```
:root {
  --bg:        #f5f3ee;  --surface: #fffdf8;  --border: #e3ded3;
  --text:      #1d1d1f;  --text-muted: #6b6b70;
  --accent:    #d6453d;  /* signal / primary action only */
  /* semantic data hues — stable meaning across the whole UI */
  --data-1:#3d7dd6; --data-2:#3aa676; --data-3:#e0a93b; --data-4:#d6453d;
}
@media (prefers-color-scheme: dark) {
  :root { --bg:#121212; --surface:#1a1a1a; --border:#2a2a2a;
          --text:#ececec; --text-muted:#9a9aa0; }
}
```

Keep the accent rare — when everything is neutral, one accent reads as *signal*.

## Type

- **Clean sans for prose**, **monospace for data, labels, code, designators.** The
  monospace/technical-caps treatment is what signals "instrument panel."
- Restrained modular scale (e.g. 13 / 15 / 18 / 24 / 32 / 48); generous line-height
  (~1.55) for body, tight for data tables.
- Use small caps or letter-spaced uppercase for section/category labels.

```
:root {
  --font-sans: ui-sans-serif, system-ui, -apple-system, sans-serif;
  --font-mono: ui-monospace, "SF Mono", "JetBrains Mono", monospace;
  --t-xs:13px; --t-sm:15px; --t-md:18px; --t-lg:24px; --t-xl:32px; --t-2xl:48px;
}
```

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
