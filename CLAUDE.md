# hvor.io — CLAUDE.md

## Project overview
Personal portfolio/hobby site for Emil Møller Rasmussen (CTO, aiknowit.dk).
Hosted at https://www.hvor.io via GitHub Pages (CNAME configured).

The site is a **single-page Danish-language portfolio** showcasing hobby apps.
The working file for active development is `index_draft.html`; `index.html` is the live version.
**Never edit `index.html` unless Emil explicitly asks.**

## Stack
- Plain HTML / CSS / vanilla JS — no build step, no framework
- **Bulma** is loaded but mostly unused — layout is now custom CSS
- **Devicons** for tech icons (CDN, v2.15.1)
- **Bootstrap Icons** for general icons (CDN)
- **Fontawesome** for brand/solid icons (local, `./static/fontawesome/`)
- **Google Fonts** — Barlow (body), VT323 (accent), Caprasimo (headlines), Chewy, Dancing Script, Playfair Display, Bangers, Chicle
- Custom `@font-face` fonts in `./static/fonts/` (enmere, omvej, solskin, regnvejr, groent, lynafleder)
- Custom styles in `./static/style.css`
- All page-specific styles live in a `<style>` block inside `<head>` of `index_draft.html`

## Page structure (current)
Full-viewport colored band sections, stacked vertically:

| Section | Color | Key content |
|---------|-------|-------------|
| Navbar | Red → frosted glass on scroll | Fixed, `site-nav` / `.frosted` class toggled by JS |
| Hero | `hsla(6,62%,52%,1)` red | Caprasimo headline "hvor.io", `-webkit-text-stroke` cartoon border |
| Splash / Intro | `#FFD255` yellow | Chat bubbles animating in on scroll (English copy, right-aligned) |
| Projekter | `hsl(152,38%,44%)` sage green | 6-column poke-card grid |
| Process | `hsl(218,40%,28%)` dark navy | Icon flow + descriptions, left title |
| Om mig | `#FBB7C0` pink | Two-column bio + fact table, `id="om"` |
| Kontakt | dark | Links + footer, `id="kontakt"` |

Section IDs for nav: `#projekter`, `#om`, `#kontakt`

## Poke-cards (project cards)
- Class: `.poke-card` on `<a>` tags — `aspect-ratio: 5/8`, `border: 8px solid #F5C518`
- Color variants: `.c-amber`, `.c-yellow`, `.c-green`, `.c-teal`, `.c-purple`, `.c-blue`
- Brand fonts per card (applied via `.poke-name.font-*` overrides in `<style>` block):
  - En mere, tak! → Chewy
  - solskin.app → Dancing Script
  - Omvej → Playfair Display italic
  - Grønt → `groent` custom font (Wonderly.otf)
  - Lynafleder → Bangers
  - REGNVEJR → Chicle

## Process section (dark navy)
- Icons from Flaticon (Freepik attribution required) stored in `./static/imgs/`:
  - `question.png`, `think.png` — stacked left, with `turn-right-arrow-svgrepo-com.svg`
  - `read.png`, `microscope.png`, `online-education.png`, `startup.png` — horizontal chain
  - `right-arrow-svgrepo-com.svg` — between horizontal icons
- All icons pop in sequentially via IntersectionObserver + `animation-play-state`
- Bottom turn-arrow uses `scaleY(-1)` on the inner `<img>` (not the animated wrapper)

## Chat bubble animation (yellow section)
- Three bubbles (`.chat-bubble.b1/b2/b3`) animate via `bubblePop` keyframe
- Triggered by IntersectionObserver adding `.chat-active` to `.splash-band`
- Copy is intentionally in **English** (user decision)

## Conventions
- **Danish** throughout, including the yellow intro chat bubbles (changed from English 2026-05-13)
- All `<style>` blocks must live inside `<head>` — never after `</head>`
- `<html lang="da">` required
- Scroll animations: `IntersectionObserver` adds `.flow-active` (process) or `.chat-active` (splash) or `.visible` (fade-in elements)

## Projects listed on site
| App | Status | Route | Brand font |
|-----|--------|-------|------------|
| En mere, tak! | aktiv | /en-mere-tak/ | Chewy |
| solskin.app | aktiv | /plads-i-solen/ | Dancing Script |
| Omvej | demo | /detour-frontend/ | Playfair Display italic |
| Grønt | demo | /groent/ | groent (Wonderly.otf) |
| Lynafleder | demo | /lynafleder/ | Bangers |
| REGNVEJR | aktiv | /regn/ | Chicle |

## Known issues / things to keep in mind
- Process section icon alignment: the merge SVG (turn arrows) is sized for 90px icons with 2rem gap — if icon size changes, update SVG height (currently 212px)
- Flaticon icons need attribution — currently not added to the page
- OG tags present; no `og:image` yet
- No favicon yet
- Dark mode media query exists but pink/yellow/process bands are not fully dark-mode aware

## Do not
- Remove the Danish copy — the site is intentionally in Danish (except the chat bubbles)
- Add a build system or bundler — keep it plain HTML
- Use Inter, Roboto, or Arial — the site uses Barlow + custom display fonts
- Edit `index.html` — always work in `index_draft.html`
