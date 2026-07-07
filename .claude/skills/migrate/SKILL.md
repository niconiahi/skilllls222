---
name: migrate
description: Migrate a scattered page — inline-style HTML, a Webflow or static export, one giant file — into the componentized system. Use when the user wants to migrate or componentize a page that isn't broken into components yet, or to rebuild static HTML/CSS as the kit.
---

# Migrate

Turn one scattered page into components. This skill is the **order**; the conventions live in the reference skills — reach for them at each step, don't restate them.

You are not designing, you are **transcribing**. The source page is the spec: every color, size, and block already exists. Your job is to relocate each one into its rightful token and component — not to redesign it. When in doubt, match the source.

Work top to bottom through the steps. Each ends on a checkable condition; don't start the next until this one holds.

## 1. Shell

The kit and the token rulers presuppose a running Next.js + Tailwind 4 project with postcss `@custom-media` wired (a `tokens.css` and a `breakpoints.css`). If that project isn't there, create it first. Done when `npm run dev` serves a page and `var(--spacing)` resolves.

## 2. Tokenize

Port the source's `:root` — and any raw value it repeats — into `tokens.css`, following **how-to-css**. Done when every color, size, and space the source uses exists as a token, and no hex or raw number survives outside a token definition.

## 3. Build the base set

Build the base components the page needs, following **eager-component**, before any section. Done when each is a `Name.tsx` + `Name.css` pair with its `hover`/`active`/`focus` states, and nothing section-specific has been built yet.

## 4. Compose, block by block

Walk the source top to bottom. Every block becomes a plain `<section>` (flex or grid, plus its decorative svgs) that composes base components and content markup; a block that runs browser JS (event handler, scroll listener, observer) is a client component. Done when **every block in the source is a `<section>`**, every reusable piece inside is a base component (nothing hand-rolled that duplicates one), and no content-bearing markup is left loose outside a section.

## 5. Localize & cache assets

Every non-photo asset the source pulls from a remote URL (an icon, logo, vector, or pattern) is downloaded into `/public/assets/` (vectors under `/public/assets/vectors/`), and its component repointed at the local file. Photos may stay on their CDN.

That tree is served **immutable**: put a one-year `Cache-Control: public, max-age=31536000, immutable` on `/assets/*`. This is only safe because assets are **content-addressed** — never edit an asset in place, rename it to change it. Done when no component references a remote URL for a vector, and `/assets/*` carries the immutable cache header.

## 6. QA

Run **qa** on the finished page and resolve what it reports. Done when qa finds no violations.
