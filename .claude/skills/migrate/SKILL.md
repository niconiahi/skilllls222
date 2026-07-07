---
name: migrate
description: Migrate a scattered page — inline-style HTML, a Webflow or static export, one giant file — into the componentized system. Use when the user wants to migrate or componentize a page that isn't broken into components yet, or to rebuild static HTML/CSS as the kit.
---

# Migrate

Turn one scattered page into components. This skill is the **order**; the conventions live in the reference skills — reach for them at each step, don't restate them.

You are not designing, you are **transcribing** — but transcribe the *look*, not the markup. Every color, size, and block already exists in the source; relocate each into its rightful token and component and match the source visually. Its DOM, though, is noise: strip the nested wrapper layers and rebuild each block as the fewest elements that reproduce the look (see **eager-component** → Markup).

Work top to bottom through the steps. Each ends on a checkable condition; don't start the next until this one holds.

## The golden page first

The **home page is the golden page** — migrate it first, in full. Because it exercises the whole base set, the tokens, and the type scale, migrating it *is* how the shared system gets built. Run it all the way through the steps below, apply every rule, and commit it. Nothing else starts until the home page is closed.

The other pages then **replicate** it. The system already exists, so they reuse the setup steps (Shell, Tokenize, Type scale, Build base) instead of redoing them — each is just Compose → SEO → Localize → Match → QA. With the golden page settled, the rest can run in parallel.

## 1. Shell

The kit and the token rulers presuppose a running Next.js + Tailwind 4 project with postcss `@custom-media` wired (a `tokens.css` and a `breakpoints.css`). If that project isn't there, create it first. Done when `npm run dev` serves a page and `var(--spacing)` resolves.

## 2. Tokenize

Port the source's `:root` — and any raw value it repeats — into `tokens.css`, following **how-to-css**. Done when every color, size, and space the source uses exists as a token, and no hex or raw number survives outside a token definition.

## 3. Type scale

Look at the source's text and find its most representative sizes — the recurring heading and body sizes, not every one-off. Cluster them into the six type tokens (see **how-to-css** → Type): three headings, three body. Done when the six tokens exist, each with its minimal mobile value, none below 14px, and every piece of text maps to one of them.

## 4. Build the base set

Build the base components the page needs, following **eager-component**, before any section. Done when each is a `Name.tsx` + `Name.css` pair with its `hover`/`active`/`focus` states, and nothing section-specific has been built yet.

## 5. Compose, block by block

Walk the source top to bottom. Every block becomes a plain `<section>` (flex or grid, plus its decorative svgs) that composes base components and content markup. To place each piece, screenshot the block and pinpoint its distinct parts; for each, search the design system first and reuse a match — create a new component, local to the page or section, only when nothing fits. Copy, URLs, and hours come from `/lib/constants.ts`, not inline. A block that needs browser JS becomes a client component — but reach for HTML/CSS standards before the client (see **eager-component**). Inventory the source's `<script>` behaviors first (scroll effects, toggles, reveals) so none is dropped. Done when **every block in the source is a `<section>`**, every source behavior is reproduced, the page has exactly one `<h1>` (the hero's, on the home page), every reusable piece is an existing component reused or a deliberate new one (nothing duplicates a component that already exists), and no content-bearing markup is left loose outside a section.

## 6. SEO & metadata

Port the source `<head>` — title, description, favicon, canonical, social/OG tags — into Next's metadata API, one export per route. Every page gets its own unique title and description (see **eager-component** → Pages); never a shared default, always the best each page can carry. Done when every route exports its own metadata and no two pages share a title or description.

## 7. Localize & cache assets

Every non-photo asset the source pulls from a remote URL (an icon, logo, vector, or pattern) is downloaded into `/public/assets/` (vectors under `/public/assets/vectors/`), and its component repointed at the local file. Photos may stay on their CDN.

That tree is served **immutable**: put a one-year `Cache-Control: public, max-age=31536000, immutable` on `/assets/*`. This is only safe because assets are **content-addressed** — never edit an asset in place, rename it to change it. Done when no component references a remote URL for a vector, and `/assets/*` carries the immutable cache header.

## 8. Match the source

Screenshot the rebuilt page and the original side by side, at desktop and mobile, and compare top to bottom. You are transcribing: a difference is a defect unless you chose it. Done when the rebuilt page matches the source at both widths, or every remaining difference is deliberate.

## 9. QA

Run **qa** on the finished page and resolve what it reports. Done when qa finds no violations.
