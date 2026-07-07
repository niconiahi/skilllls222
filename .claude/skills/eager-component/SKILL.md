---
name: eager-component
description: Build UI from the fixed base component set, composed inside plain <section> layout. Use when adding, building, or changing anything on a page — a button, link, card, form, header, footer, or nav.
---

# Eager components

The user is a designer, not a developer. Explain in plain language, no code talk unless they ask.

## The base set

The list below is the shared library — the design-system components on every page. Reach for it first: **search before you build**, because we don't repeat ourselves. A block may still need a piece the library lacks — then create a component, local to its page or section. But a section wrapper or loose content markup is never a component (see **Sections**).

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

## Cards

On mobile, every card (`MenuCard`, `SpecialCard`, `BlogCard`) fills the full width of its parent — never its own width or `max-width`. That parent is the section, already capped at `--max-content`; the card just fills what the cap allows.

## Sections

A page is a sequence of plain `<section>` elements. The section is the first layer of layout — flex or grid, whichever the block needs — and it carries the decorative SVGs. Base components and content markup sit inside it. The section itself is never a component.

```tsx
<section className="…">        {/* layout: flex or grid, + decorative svgs */}
  <MenuCard … />
  <MenuCard … />
</section>
```

## Pages

Each page carries two things of its own:

- **One `<h1>`** — exactly one per page. On the home page it lives in the hero section.
- **Its own SEO** — every page sets a unique `title` and `description` (Next metadata), plus social/OG tags. Never a shared default; the best metadata each route can carry.

## Structure

Each component is a `Name.tsx` + `Name.css` pair, side by side. Markup uses plain semantic class names — no Tailwind utilities. Every color, space, and size comes from a token (`var(--…)`); Tailwind exists only to supply those tokens.

## Markup

Fewest elements wins. A component is the smallest tree that renders the design — never wrapper-upon-wrapper just to position something. Positioning, alignment, and spacing come from CSS (flex, grid, `position`) on the elements that already hold content, not from extra layers of `<div>`. If an element exists only to push another one around, delete it and do it in CSS.

**Compound** components (Hamburger, Formulary) expose their parts as `Parent.Child` — a form is assembled from `Formulary.Label` + `Formulary.Input` and friends, never from loose markup.

## Content

Copy, URLs, hours — all user-facing text lives in one module, `/lib/constants.ts`. Components import their content from it; nothing user-facing is hardcoded in markup, so one edit changes it everywhere.

## Interactive states

Every clickable surface — a Button, a Link, anything tappable — is **at least 48px tall** (the minimum tap target), and its CSS defines `hover`, `active`, and `focus`. Hover is mandatory: a clickable surface with no hover is not done.

## Current link

A Link that points at the page you're on gets a **current** marker — `aria-current="page"` plus styling that sets it apart from the rest. The nav always shows where you are. Required, not optional.

## Motion

Everything moves. Interactive components animate on interaction; static content — every card, every image — gets an entrance or micro-animation, so the page never sits still. Static is no excuse to skip motion: a block that doesn't move is not done.

All of it respects `prefers-reduced-motion`: when the user asks for less, the motion stops. Mandatory motion with no off-switch is an accessibility defect.

## Rendering & behavior

Default to server components — ship HTML, not JavaScript. Reach for HTML and CSS standards first: `<details>` for a disclosure, `:target` and anchor links, a native `<form>`, CSS transitions and scroll-driven animation. Only a behavior that genuinely needs JavaScript — an event handler, a scroll listener, an `IntersectionObserver` — makes its component a client component (`"use client"` at the top of the file). The client is the last resort, one component at a time; everything around it stays on the server.
