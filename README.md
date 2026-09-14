# Gems in Bali 🌴

A travel-companion web app for exploring Bali beyond the tourist trail — ask an
AI-style question box where to go, get a full adventure plan (transport,
itinerary, live trip mode), then share your experience and level up as a
trusted local contributor.

This is a **working front-end prototype**. All data (destinations, community
posts, AI answers) is mocked in `src/data/mockData.js` so the whole flow works
immediately with no API keys or backend. It's built so swapping in real
services later is a matter of replacing a few functions, not rewriting pages.

## Tech stack

- React 18 + Vite
- React Router (client-side routing)
- Tailwind CSS
- Plain React Context + localStorage for user state (XP, level, posts) — no
  backend required to try it out

## Pages / flow

| Route | What it is |
|---|---|
| `/` | Cover page — hero + AI question box + popular destinations |
| `/explore` | Full Bali map with tag filters |
| `/plan/:id` | AI-generated adventure plan (budget, level, activities, transport summary) |
| `/transport/:id` | Deeper transportation options with route steps |
| `/itinerary/:id` | Full-day itinerary timeline |
| `/trip/:id` | Live "during the trip" mode — ETA, nearby places, notifications |
| `/community` | Community feed — posts, likes, comments |
| `/community/new` | Share your experience — photos, review, AI-suggested tags, XP |
| `/tags` | Browse destinations by tag (river, rafting, warung, budget, etc.) |
| `/profile` | XP, level, contributed places, credibility |
| `/business` | Ad/listing plans for local businesses to appear on the map |

## Running locally

```bash
npm install
npm run dev
```

Then open the printed local URL (usually `http://localhost:5173`).

## Building for production

```bash
npm run build
npm run preview   # to test the production build locally
```

## Pushing to GitHub

```bash
git init
git add .
git commit -m "Initial commit: Gems in Bali prototype"
git branch -M main
git remote add origin https://github.com/<your-username>/gems-in-bali.git
git push -u origin main
```

## Where to plug in real services next

- **AI planning** — replace `mockAskAI()` in `src/data/mockData.js` with a real
  call to your AI provider (e.g. the Anthropic API). Keep the same return
  shape (a destination object) and every page downstream keeps working.
- **Maps** — `src/components/BaliMap.jsx` is a stylized stand-in. Swap its
  `<svg>` for Google Maps / Mapbox and keep the same `destinations` prop shape
  (`{ coords: { x, y } }` → real lat/lng).
- **Live trip notifications** — `TripMode.jsx` currently fakes ETA/notifications
  with a timer. Replace with real geolocation + a push/WebSocket feed.
- **Backend & auth** — `AppContext.jsx` currently persists to `localStorage`.
  Swap its functions for API calls once you have a backend + user accounts,
  and posts/XP will sync across devices instead of staying on one browser.
- **Business ads** (`/business`) — currently a static pricing page. Wire the
  "Get started" buttons to a real checkout/subscription flow when ready.

## Design

Palette and type choices are documented as comments in `tailwind.config.js`
and `src/index.css` — built around a Bali identity (rice-terrace green, temple
gold, volcanic black) rather than generic SaaS defaults.
