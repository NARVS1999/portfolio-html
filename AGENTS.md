# AGENTS.md

Static single-page portfolio. Four standalone HTML files, no build system, no package manager, no tests. Run/verify by opening the HTML file directly in a browser.

## File variants

Each file is a complete, self-contained variant of the same portfolio — all CSS in one `<style>` block, all JS in one IIFE at the bottom, no partials. They are independent variants, not a merge chain:

- `index.html` — original newspaper theme (Outfit / Yusei Magic fonts). 3 animated dogs, flower/tree canvas, MyCourses link, older copy ("3+ years").
- `neo-brutalism.html` — neo-brutalist restyle of index (Archivo Black / Space Grotesk), same content, still has flowers + 3 dogs.
- `neo-brutalism-v2.html` — v1 + modern touches: marquee ticker, rotated stickers, back-to-top, snap easing, dot-grid card. No flowers, only the small dog, no MyCourses link.
- `neo-brutalism-v3.html` — v2 design, content mirrors the resume (4 years experience, categorized Core Skills, metric job bullets, ADSvanced dated Oct 2023). Newest/most current copy; index–v2 still carry older content.

## Conventions

- Brutalist files define the palette as CSS custom properties in `:root` + `body.dark`. `index.html` instead duplicates every rule under `.newspaper.dark` — do not mix the two approaches.
- Dark mode JS toggles `body.dark` **and** `.newspaper.dark`; twinkling stars only spawn in dark mode.
- Theme toggle square: track is `36x20` with `2px` border, thumb travels `translateX(18px)` — changing switch dimensions requires updating both the inline HTML styles and that JS value.
- Skill chips are `.tech-grid .curriculum-item[data-tech="..."]`; every `data-tech` value must have a matching key in the inline `techDescriptions` object or its modal shows fallback text.
- Job history lives in `.work-item` blocks: `job-desc` is click-toggled (v3 uses `<ul>` bullets), `data-label` is the toast text.
- Asset paths are relative (`assets/images/...`, `assets/audio/...`) — files must stay at repo root next to the HTML.
- Full render needs internet (Google Fonts + Bootstrap Icons CDNs); offline it degrades to fallback fonts/icons.
- Dog animation uses frames `dog_run_0..4.png` (`FRAME_COUNT = 5`; `dog_run_5.png` exists but is unused). Flower canvas (`grow_0..5.png`, `treeCanvas`) exists only in index + neo-brutalism v1.
- Adding/renaming a variant = copy an existing file, then edit in place; each file's title tag carries its variant name (e.g. `Neo-Brutalism V3`).

## Verification

No lint/test tooling exists. After edits: open the file in a browser, and sanity-check tag balance (`div`/`span`/`ul`) plus CSS `{}` balance — Python 3 is available for a quick one-off script.

## Content source

Copy mirrors the resume at `C:\Users\Admin\Downloads\JOHN_PAUL_NARVASA_-_CV-102026.docx.pdf`. PDFs cannot be read directly by the model; extract text with `pdftotext -layout "<path>" -` (available in this environment).

## Git

Local-only, no remote. History is concise lowercase messages (e.g. `initial setup`, `add neo-brutalist portfolio variants v1-v3`). Only the four HTML files and `assets/` are tracked/relevant; don't commit temp scripts.
