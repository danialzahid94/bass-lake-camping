# The Camping Checklist - Public Packing Checklist Website

## Project Overview
A free, public camping checklist website. Originally built as a real-time trip planner for a specific group trip to Bass Lake Provincial Park (May 2026); after that trip concluded, it was repurposed into a general-purpose, standalone packing checklist that anyone can use and share. No trip-specific or group-specific content remains.

## Architecture
- **Hosting:** GitHub Pages (static site, free)
- **Frontend:** Single HTML file with embedded CSS and JS (no build tools, no framework)
- **Persistence:** Browser `localStorage` only — checked items are saved locally per visitor. There is no backend and no shared/collaborative data; this is intentional since the site is public (anyone with the link can visit, and visitors should not see or affect each other's checklists).

## Tech Stack
- Vanilla HTML/CSS/JavaScript
- No npm, no bundler, no framework, no database — intentionally simple for easy maintenance

## GitHub Pages Deployment
- `.github/workflows/deploy.yml` deploys `index.html` straight to GitHub Pages on every push to `main` (checkout → upload artifact → deploy). No build step, no secrets required.
- Repo Settings > Pages > Source: GitHub Actions.

## Site Structure (Single Page)
All sections are in `index.html` with smooth-scroll navigation:

1. **Hero** — Title and tagline explaining the tool
2. **Toolbar** — Overall progress bar ("X of Y items packed"), Print button, Reset button
3. **Essentials** — 8 categories (~49 items): Shelter & Sleep, Kitchen & Food, Fire, Light & Power, Clothing, Hygiene & Health, Navigation & Safety, Camp Comfort
4. **Essentials for Kids** — Gear for camping with children (~14 items)
5. **Essentials for Cold Weather** — Cold-specific gear (~11 items)
6. **Essentials for Hot Weather** — Heat-specific gear (~10 items)
7. **Other Items** — Optional nice-to-haves (~10 items)
8. **Footer** — Leave No Trace reminder + note that data stays local to the browser

Each checkbox has a stable id (`sectionId__groupSlug__itemSlug`) and is tracked in a single `localStorage` key (`campingChecklistState`). Section and per-category header badges show live "checked/total" counts, computed by re-scanning checkbox state (no separate synced state object). Print styles (`@media print`) hide the header/toolbar/footer for a clean printable list.

## Design
- **Theme:** Outdoorsy & warm
- **Colors:** Earthy greens (#2D5016, #4A7C28), browns (#5C4033, #8B6914), campfire oranges (#E8820C, #D46B08), cream backgrounds (#FDF6E3, #FAF0DC)
- **Responsive:** Mobile-friendly, works on all screen sizes
- **Font:** System fonts (Segoe UI stack)

## Known Issues / Notes
- No authentication, no accounts, no analytics — fully static and anonymous.
- Checklist state is per-browser (localStorage), so it does not follow a visitor across devices and clears if site data/cache is cleared.
- The checklist content (categories and items) lives in the `sections` array in the inline `<script>` — edit there to add/remove/reword items rather than hand-editing rendered HTML.

## File Structure
```
bass-lake-camping/
  index.html                       — The entire site (HTML + CSS + JS)
  Claude.md                        — This file (project context)
  .github/workflows/deploy.yml     — GitHub Pages deploy workflow
```
