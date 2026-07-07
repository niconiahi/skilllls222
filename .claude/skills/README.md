# Design-system migration skills

These skills turn a scattered, un-componentized web page (inline-style HTML, a Webflow or static export) into a clean, componentized **Next.js + Tailwind 4** design system — and then govern every page built on it.

## The intended skills

Six skills form this set. **`migrate` is the entry point**; it orchestrates the other five. Everything is authored here (real directories); anything else in this folder is a general-purpose skill symlinked in from another collection and is **not** part of this set (e.g. `grilling`, `research`, `tdd`, `teach`, `to-prd`, `writing-great-skills`).

| Skill | Role | Reach for it when |
|---|---|---|
| **migrate** | Orchestrator — the ordered process for a whole migration. | Turning a scattered/static page into components. The entry point. |
| **eager-component** | The component & page model: base set, sections, markup, rendering, motion, pages. | Building or changing any UI. |
| **how-to-css** | How CSS is written: tokens only, the spacing / size / type rulers, the content cap. | Writing or editing any CSS. |
| **qa** | Single-page review against the rules. | Checking a finished page. |
| **vector-backgrounds** | Placing an SVG as a tiled section background. | An svg goes behind a section. |
| **vector-decorations** | Placing an SVG as a positioned accent. | An svg accent sits on or near an element. |

## How they fit together

`migrate` is the spine; its steps call the others:

- **Conventions** — `eager-component` (structure) and `how-to-css` (styling) are the two rulebooks every step obeys. They are the single source of truth; `migrate` points to them rather than restating them.
- **Assets** — `vector-backgrounds` / `vector-decorations` place SVGs. During a migration you transcribe the existing `<img>` vectors (localizing their source); the skills' interactive designer-in-the-loop flow is for steady-state work, not the autonomous migration.
- **Check** — `qa` reviews the finished page.

## The model in one screen

Detail lives in the skills — this is the map.

- **Components** — one shared **base set**: `Button` (`primary`/`secondary`/`outline`), `Link`, `Header`, `Footer`, `Hamburger`\*, `Formulary`\*, `MenuCard`, `SpecialCard`, `BlogCard` (\* = compound, `Parent.Child`). Search it first (DRY); create a page/section-local component only when nothing fits. A section wrapper or loose content is never a component.
- **Layout** — a page is a sequence of plain `<section>` elements (flex or grid + decorative svgs) composing components. Markup is the fewest elements possible; positioning is CSS, never nested wrappers. Cards fill their parent's width on mobile.
- **Tokens** — brand colors, the `--spacing` small ruler (margins/paddings/gaps/separations/heights), the size ruler (large fixed dimensions), the six-token **type scale** (`heading`/`body` × `sm`/`md`/`lg`, 14px floor, barely responsive), `--max-content`, section separations, breakpoint tokens. No magic values.
- **Standing rules** — content never exceeds `--max-content`; clickable surfaces are ≥48px tall with mandatory hover; the current-page link is marked (`aria-current`); everything animates, respecting `prefers-reduced-motion`; one `<h1>` per page (the hero's on home); every page has unique SEO; all copy lives in `/lib/constants.ts`; server-first — client JS is the last resort.

## Golden-page workflow

Migrate the **home page first, in full** — it is the golden page whose migration builds the shared system (base set, tokens, type scale). Commit it once closed. Every other page then **replicates** it, reusing the setup steps, so the rest can run in parallel.

## The nine steps

`migrate` runs, in order:

**Shell → Tokenize → Type scale → Build base → Compose → SEO → Localize & cache → Match source → QA**
