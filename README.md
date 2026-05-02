# gpalette

A small React color palette explorer — browse curated palettes (Material UI + 8 Flat UI variants), click a swatch to copy the hex code with a sound, an animated overlay, and a randomly-picked encouragement.

🎨 **Live demo:** **[gpalette.vercel.app](https://gpalette.vercel.app)**

> My very first React project — built during my eKreative front-end internship as the final exercise of the CRA series. Originally lived inside the [Practice_Ek](https://github.com/B1toks/Practice_Ek) monorepo and was extracted into this standalone repo for clarity.

## What it does

- **Home page** with a grid of palette previews (each preview shows a few sample swatches)
- **9 detail routes**, one per palette family:
  - Material UI Colors
  - Flat UI Colors v1 / Dutch / American / Aussie / British / Spanish / Indian / French
- **Click any swatch** to:
  1. Copy the hex code to the clipboard (`navigator.clipboard.writeText`)
  2. Play a short notify sound
  3. Display a full-screen tinted overlay with a random encouraging phrase ("Way to go!", "Great job!", "You nailed it!", …)
- Animated route transitions (`react-transition-group`) — each navigation fades smoothly
- All palette data is JSON-driven (`public/palette.json`), so adding a new palette is just a JSON entry + one route component

## Tech

- **React 18** + Create React App
- **react-router-dom v6** — routing between Home and palette pages
- **react-transition-group** — `CSSTransition` + `TransitionGroup` for route animations
- **Clipboard API** — `navigator.clipboard.writeText` for copying hex codes
- **HTMLAudioElement** — `new Audio(...).play()` for the notify sound
- Hand-written CSS — no framework, no UI kit
- Static palette data via `fetch('palette.json')` from `public/`

## Run locally

```bash
git clone https://github.com/B1toks/gpalette.git
cd gpalette
npm install
npm start
```

Then open <http://localhost:3000>.

Build for production:

```bash
npm run build
```

## Project structure

```
public/
├── index.html
├── manifest.json
├── palette.json          ← all palette data (name + colors)
├── src_notify.mp3        ← notification sound played on copy
└── img/                  ← decorative tile background

src/
├── index.js              ← app entry: Router + Routes for all palettes
├── index.css             ← global styles
├── App.js                ← (legacy) early version — actual rendering happens in index.js
├── App.css
├── MaterialUIColors.js   ← detail page for Material UI Colors
├── FlatUIColorsv1.js     ← detail page for Flat UI v1
├── FlatUIColorsAmerican.js
├── FlatUIColorsAussie.js
├── FlatUIColorsBritish.js
├── FlatUIColorsDutch.js
├── FlatUIColorsFrench.js
├── FlatUIColorsIndian.js
└── FlatUIColorsSpanish.js
```

## What I focused on

This was my first time wiring multiple things together in React:

- **State + side effects** — `useState` + `useEffect` to fetch palette data once on mount and store it in state
- **Routing** — multi-page SPA with `react-router-dom` v6 (Routes / Route / Link / `useLocation`)
- **Route animations** — wrapping `<Routes>` in `<CSSTransition>` keyed off `location.key`
- **Browser APIs** — Clipboard for copy, HTMLAudioElement for sound, dynamically-created DOM nodes for the overlay
- **Composition** — splitting palette pages into separate components and feeding them all the same JSON

Built by **Oleksandr Honchar** — [www.honchar.dev](https://www.honchar.dev) · [GitHub](https://github.com/B1toks)
