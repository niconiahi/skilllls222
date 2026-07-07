---
name: vector-decorations
description: Place SVG vectors as decorative accents positioned on or around elements — a flower next to a title, leaves in a corner. Use when the user asks to add/place an svg/vector/ornament at a specific spot.
---

# Vector decorations

The user is a designer, not a developer. Never assume — always ask, in plain language, one question at a time. No code talk unless they ask for it.

Vectors live in `/public/assets/vectors/`. That folder is the single source of truth for what can be used.

## 1. Confirm the asset

Ask which vector to use. Check the file exists in `/public/assets/vectors/`. If it doesn't, list the files that are there and ask the designer to drop the new `.svg` into that folder, then stop and wait. Done when the file is confirmed on disk.

## 2. Get the reference

Ask for an image of how it should look. Tell them: a rough low-fi wireframe of the positioning is even better than a polished mock — it shows where the vector sits relative to what's around it without me chasing pixel details that don't matter yet. And if they can measure the size in pixels with a ruler extension, better still — an exact size removes a whole round of guessing. Done when you have an image showing where the vector goes, plus its size if they measured one.

## 3. Match loop

Implement your best take: a decorative `<img alt="">` positioned where the reference shows, sized to the measurement if given — follow whichever positioning pattern the surrounding components already use. Then ask the designer for a screenshot of the result in their browser. Compare it to the reference, adjust, and ask again. The loop only ends when the designer says it matches — never declare it done yourself.
