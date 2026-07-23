# Salitan — Pickleball Open Play

A tiny, offline-first web app for running fair **2v2 pickleball open play**. It manages the paddle queue, rotates players onto courts, tracks scores and standings, and shares results with the group — all from a phone, no install or account required.

*"Salitan" means taking turns — which is the whole point: everybody gets a fair, rotating game.*

## Features

- **Paddle queue / stacking rotation** — add players, and Salitan builds balanced 2v2 matchups and rotates the next group on as courts free up.
- **Multiple courts** — run several courts at once; each shows the current match and who's up next.
- **Players & breaks** — mark players on break so they're skipped in the rotation, then bring them back.
- **Scores, standings & match log** — record results, see live standings, and review full match history.
- **Session wrap-up** — finish a session to get final standings and a shareable summary for the group.
- **Live sharing** — share the session (QR code) so others can follow along.
- **Installable PWA** — add to home screen; works offline thanks to a service worker cache.

## Run it

It's a single static page — no build step.

- **Hosted:** open the deployed URL on your phone and *Add to Home Screen*.
- **Local:** serve the folder over HTTP (a service worker needs `http`, not `file://`):
  ```bash
  npx serve .        # or: python3 -m http.server
  ```
  Then open the printed `localhost` URL.

## How it works

Everything runs in the browser. Session state (players, courts, scores) is kept in `localStorage`, so a refresh won't lose your game. `sw.js` caches the app shell **network-first** for the page (so updates land) with a cache fallback (so it keeps working with no signal on the court). Live sharing pulls the QR library from a CDN and, when enabled, syncs over the network.

## Tech

Plain HTML/CSS/JS in a single `index.html`, a service worker (`sw.js`), and a web manifest — no framework, no bundler.

| File | Role |
|---|---|
| `index.html` | The whole app — UI, rotation logic, state |
| `sw.js` | Service worker: offline cache + update strategy |
| `manifest.webmanifest` | PWA metadata (name, icons, theme) |
| `icon-192.png`, `icon-512.png` | App icons |

## License

[MIT](./LICENSE) © 2026 Sef
