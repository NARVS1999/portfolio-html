# AGENTS.md

Static single-page portfolio. Five standalone HTML files (four portfolio variants + one LinkedIn cover), no build system, no package manager, no tests. Run/verify by opening the HTML file directly in a browser.

## File variants

Each portfolio file is a complete, self-contained variant — all CSS in one `<style>` block, all JS in one IIFE at the bottom, no partials. They are independent variants, not a merge chain:

- `index.html` — **canonical/current**: neo-brutalist design (ticker, stickers, back-to-top, dot-grid card), content mirrors the resume (4 years experience, categorized Core Skills, metric job bullets, ADSvanced dated Oct 2023). Contact uses flex `.c-row` rows; summary is single-column. Title tag still reads `Neo-Brutalism V3`.
- `index-v1.html` — original newspaper theme (Outfit / Yusei Magic fonts). 3 animated dogs, flower/tree canvas, MyCourses link, older copy ("3+ years").
- `neo-brutalism.html` — neo-brutalist restyle of old index (Archivo Black / Space Grotesk), same older content, still has flowers + 3 dogs.
- `neo-brutalism-v2.html` — v1 + modern touches: marquee ticker, rotated stickers, back-to-top, snap easing. No flowers, only the small dog, no MyCourses link. Older content.
- `linkedin-cover.html` — fixed 1584×396 LinkedIn banner, theme only, no JS. Bottom-left zone must stay clear (LinkedIn avatar overlaps it); screenshot via DevTools *Capture node screenshot*.

## Conventions

- Brutalist files define the palette as CSS custom properties in `:root` + `body.dark`. `index-v1.html` instead duplicates every rule under `.newspaper.dark` — do not mix the two approaches.
- Dark mode JS toggles `body.dark` **and** `.newspaper.dark`; twinkling stars only spawn in dark mode.
- Theme toggle square: track is `36x20` with `2px` border, thumb travels `translateX(18px)` — changing switch dimensions requires updating both the inline HTML styles and that JS value.
- Skill chips are `.tech-grid .curriculum-item[data-tech="..."]`; every `data-tech` value must have a matching key in the inline `techDescriptions` object or its modal shows fallback text.
- Job history lives in `.work-item` blocks: `job-desc` is click-toggled (index.html uses `<ul>` bullets), `data-label` is the toast text.
- `index.html` contact info uses flex `.c-row` rows to keep each icon glued to its text — don't revert to `<br>`-separated lines (the email row wraps apart in the 200px column otherwise).
- Asset paths are relative (`assets/images/...`, `assets/audio/...`) — files must stay at repo root next to the HTML.
- Full render needs internet (Google Fonts + Bootstrap Icons CDNs); offline it degrades to fallback fonts/icons.
- Dog animation uses frames `dog_run_0..4.png` (`FRAME_COUNT = 5`; `dog_run_5.png` exists but is unused). Flower canvas (`grow_0..5.png`, `treeCanvas`) exists only in index-v1 + neo-brutalism v1.
- Adding/renaming a variant = copy an existing file, then edit in place; each file's title tag carries its variant name (e.g. `Neo-Brutalism V3` on index.html).

## Verification

No lint/test tooling exists. After edits: open the file in a browser, and sanity-check tag balance (`div`/`span`/`ul`) plus CSS `{}` balance — Python 3 is available for a quick one-off script.

## Content source

Copy mirrors the resume at `C:\Users\Admin\Downloads\JOHN_PAUL_NARVASA_-_CV-102026.docx.pdf`. PDFs cannot be read directly by the model; extract text with `pdftotext -layout "<path>" -` (available in this environment).

## Git

Local-only, no remote. History is concise lowercase messages (e.g. `initial setup`, `add neo-brutalist portfolio variants v1-v3`). Only the HTML files and `assets/` are tracked/relevant; don't commit temp scripts.
