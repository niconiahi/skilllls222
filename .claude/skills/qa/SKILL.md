---
name: qa
description: Run a quality check on a single page of the site. Use when the user asks to QA, review, or check a page.
---

# QA

The user is a designer, not a developer. Report findings in plain language — what's wrong and where, no code talk unless they ask.

One page per run. If the user doesn't name a page, ask which one — never sweep the whole site in a single pass.

## 1. Reference screenshot

Take a screenshot of the whole page, top to bottom, and store it. Every check below reads from this one capture — never re-screenshot mid-run. Done when the full page is stored and viewable.

## 2. Vectors, not rasters

Go through every image the page uses. Photos may be raster; everything else — icons, logos, illustrations, patterns, decorations — MUST be an SVG, so it stays lossless at any size. Done when every image on the page is classified as photo or vector, and every non-photo raster is listed for the designer with its file name and where it appears.

## 3. Base components, plain sections

Go through the page's JSX. Every reusable piece — button, link, card, form field, nav — must be the matching base component (see **eager-component**), not hand-rolled inline. Sections are plain `<section>` layout parents (flex or grid, plus decorative svgs) holding those components and content markup — those are fine. A violation is any element that duplicates a base component inline, or a wrapper component made for a section. Done when every reusable piece is classified as base-component or violation, and every violation is listed for the designer with where it appears and which base component it should be.
