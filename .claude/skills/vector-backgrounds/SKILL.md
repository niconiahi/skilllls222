---
name: vector-backgrounds
description: Place SVG vectors as decorative backgrounds on a section. Use when the user asks to put an svg/vector/pattern/illustration behind or around a section of the site.
---

# Vector backgrounds

The user is a designer, not a developer. Never assume — always ask, in plain language, one question at a time. No code talk unless they ask for it.

Vectors live in `/public/assets/vectors/`. That folder is the single source of truth for what can be used.

## 1. Confirm the asset

Ask which vector to use. Check the file exists in `/public/assets/vectors/`. If it doesn't, list the files that are there and ask the designer to drop the new `.svg` into that folder, then stop and wait. Done when the file is confirmed on disk.

## 2. Get the reference

Ask for an image of how it should look. Tell them: a rough low-fi wireframe is even better than a polished mock — it shows placement and size without me chasing pixel details that don't matter yet. And if they can measure the vector's height and width in pixels with a ruler extension, better still — exact dimensions remove a whole round of guessing. Done when you have an image showing where the vector goes relative to the section's content, plus its dimensions if they measured them.

## 3. Match loop

Implement your best take. The background MUST be applied as a class named `.{name}-pattern` after the vector (e.g. `sunflower.svg` → `.sunflower-pattern`), defined in `/styles/background.css` — never inline, never anywhere else. The technique is tiling: `background-repeat` with a small SVG, sized via `background-size` (use the measured dimensions from step 2), so the asset stays light instead of one huge graphic. If the repeat shows visible seams, the SVG itself isn't a seamless tile — tell the designer so they can export one that tiles cleanly. Then ask the designer for a screenshot of the result in their browser. Compare it to the reference, adjust, and ask again. The loop only ends when the designer says it matches — never declare it done yourself.
