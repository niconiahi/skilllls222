---
name: how-to-css
description: How CSS is written on these sites — tokens only, no magic values. Use whenever writing or editing any CSS.
---

# How to CSS

**No magic values.** No raw number, no raw size, no raw hex — nothing typed directly into a rule. Every value exists as a token first and is applied with `var(…)`. If a value isn't a token yet, make it one, then use it.

## Spacing — the small ruler

The unit is Tailwind's: `--spacing: 0.25rem` (4px). All small values — margins, paddings, gaps, font sizes — are multiples of it:

```css
padding: calc(var(--spacing) * 4); /* 16px */
```

## Sizes — the big ruler

Fixed large dimensions (card widths, hero heights, content caps) never come from spacing math — no `calc(var(--spacing) * 260)`. They come from the predefined size scale, t-shirt named, taken from Tailwind's container scale:

```css
--size-xs: 20rem;  --size-sm: 24rem;  --size-md: 28rem;  --size-lg: 32rem;
--size-xl: 36rem;  --size-2xl: 42rem; --size-3xl: 48rem; --size-4xl: 56rem;
```

Pick the nearest size — a value that isn't on the ruler doesn't exist. If nothing genuinely fits, extend the scale with a new token; never inline the number.

## Colors

Named tokens only (`var(--olive-black)`). A hex belongs in the token definition and nowhere else.

## Content cap

**No content on any page is ever wider than `--max-content`.** This one token is what keeps every page aligned — treat it as essential, never optional. It is applied through one class, `.content-cap`: a full-bleed band whose content is centered and capped at `var(--max-content)` purely by padding, no inner wrapper elements. Every band gets that class — header, sections, footer, all of them. Never give a component its own bespoke `max-width`; if it needs the cap, it wears the class.

## Media queries

Breakpoints are `@custom-media` tokens defined once in `breakpoints.css`, used by name:

```css
@media (--mobile) { … }
```

Never a raw `(max-width: 767px)` in component CSS. A new breakpoint means a new `@custom-media` token, not an inline query.

## Values without a ruler

The four rulers above are exhaustive for spacing, sizes, colors, and breakpoints. Other properties — line-height, letter-spacing, border-radius, box-shadow, transition timing, z-index — have no scale. Same discipline, lighter touch: a value that **repeats** becomes a token (`--radius-pill`, `--z-nav`, `--ease-base`); a genuine one-off may stay raw. The magic-value ban bites on the second use, not the first.
