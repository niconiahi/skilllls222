---
name: eager-component
description: Build UI from the fixed base component set, composed inside plain <section> layout. Use when adding, building, or changing anything on a page — a button, link, card, form, header, footer, or nav.
---

# Eager components

The user is a designer, not a developer. Explain in plain language, no code talk unless they ask.

## The base set

There is one fixed set of components — the whole library. You never wonder whether something is a component: it is, only if it's on this list. Everything else is section layout or content markup (see **Sections**). Reuse before creating; never invent a sibling.

- **Button** — every call-to-action. Three variants only: `primary`, `secondary`, `outline`.
- **Link** — plain text links: one look. Anything styled as a button is a **Button**.
- **Header** — top-of-page nav chrome.
- **Footer** — logo, links, social, newsletter.
- **Hamburger** — the mobile menu toggle. **Compound**: `Hamburger.Open`, `Hamburger.Close`, ….
- **Formulary** — every form; nothing form-shaped is built outside it. **Compound**: `Formulary.Input`, `Formulary.Label`, ….
- **MenuCard** — a menu-item card.
- **SpecialCard** — a feature / special card.
- **BlogCard** — a blog-post card.

That is the whole set. A `Hero`, a `Mimosas`, a `SectionIntro` — noise. Don't make them.

## Sections

A page is a sequence of plain `<section>` elements. The section is the first layer of layout — flex or grid, whichever the block needs — and it carries the decorative SVGs. Base components and content markup sit inside it. The section itself is never a component.

```tsx
<section className="…">        {/* layout: flex or grid, + decorative svgs */}
  <MenuCard … />
  <MenuCard … />
</section>
```

## Structure

Each component is a `Name.tsx` + `Name.css` pair, side by side. Markup uses plain semantic class names — no Tailwind utilities. Every color, space, and size comes from a token (`var(--…)`); Tailwind exists only to supply those tokens.

**Compound** components (Hamburger, Formulary) expose their parts as `Parent.Child` — a form is assembled from `Formulary.Label` + `Formulary.Input` and friends, never from loose markup.

## Interactive states

Every clickable surface — a Button, a Link, anything tappable — is **at least 48px tall** (the minimum tap target), and its CSS defines `hover`, `active`, and `focus`. Hover is mandatory: a clickable surface with no hover is not done.

## Current link

A Link that points at the page you're on gets a **current** marker — `aria-current="page"` plus styling that sets it apart from the rest. The nav always shows where you are. Required, not optional.

## Motion

Everything moves. Interactive components animate on interaction; static content — every card, every image — gets an entrance or micro-animation, so the page never sits still. Static is no excuse to skip motion: a block that doesn't move is not done.

## Behavior

A component that runs browser JS — an event handler, a scroll listener, an `IntersectionObserver` — is a client component: `"use client"` at the top of its file. Static components stay on the server. Guess wrong and the page crashes, so decide it per component as you build.
