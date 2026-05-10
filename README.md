# city-simulator

A **Phaser-based isometric city simulator** that A/B-compares routing
strategies for restaurant choice, with a real-time **Google Maps
heatmap** of crowd density and **six comparison charts** of
user-experience metrics. Built as the visualization piece of the
[Crowdless](https://github.com/AlexTuring010/crowdless) project.

> 🥇 Part of the team's **1st place** entry at **AI Hackathon 2026 —
> Open Track** (ACE @ AUEB, March 2026).

## What it is

Two sims run side by side, deterministically (seed `crowdless2026`):

| Side | Strategy | Picks restaurants by... |
|---|---|---|
| **Baseline — No App** | `NearestRestaurantGoal` | Closest physical restaurant only |
| **Crowdless AI — With App** | `AIRecsRestaurantGoal` | Distance + current crowdedness + queues |

NPCs spawn, pathfind through the isometric city, queue at restaurants,
and either get served or abandon. A live Google Maps overlay heatmaps
crowd density per restaurant in real time. Six Chart.js charts compare
the two sims on:

- Walk distance to store
- Crowdedness at arrival
- Queue length at arrival
- Queue abandonments
- Customers served per store
- Bad-experience events per user

The visualization made the case for what a crowd-aware app like
Crowdless does to a city's flow.

## ⚠ Honest framing — the "AI" is not ML

`AIRecsRestaurantGoal.js` is a **deterministic, hand-coded heuristic**
that emulates what a Crowdless recommender would output. There is **no
trained model**, no learning loop, no training data. It's a stand-in
designed to faithfully represent the *intent* of the app being demoed.

We built this as the visual WOW factor for the hackathon pitch. It's a
real simulator — pathfinding, queues, abandonment, metrics, all
implemented — but the "AI" lever is a hand-tuned policy, not a learned
one. Treat it accordingly.

## Stack

- **Game engine:** [Phaser 3](https://phaser.io/) (arcade physics
  build, loaded via CDN)
- **Maps + heatmap:** Google Maps JavaScript API with `visualization`
  and `geometry` libraries
- **Charts:** Chart.js (CDN)
- **Code:** Plain ES modules — no bundler, no `package.json`
- **Map data:** `map.json` (Tiled-format, ~280 KB), centered on Athens
  (37.9838, 23.7275)

## Run locally

You'll need a **Google Maps JavaScript API key** with `visualization`
and `geometry` libraries enabled. Restrict the key to your dev
referrers (`http://localhost`, `http://127.0.0.1`) before using it
anywhere — never ship an unrestricted Maps key.

1. Open `index.html` and replace the placeholder:
   ```html
   <script async
     src="https://maps.googleapis.com/maps/api/js?key=YOUR_GOOGLE_MAPS_API_KEY&libraries=visualization,geometry">
   </script>
   ```
   with your own key.
2. Serve the directory over HTTP (Maps + module imports won't work
   from `file://`):
   ```bash
   python -m http.server 8000
   # then open http://localhost:8000
   ```

## Team

Same five-person team as [Crowdless](https://github.com/AlexTuring010/crowdless):

- **Alexandros Gkiafis** ([@AlexTuring010](https://github.com/AlexTuring010))
  — simulator (this repo)
- **Theodoros Exarchos** ([@EXARTeo](https://github.com/EXARTeo))
- **Mariglena Reci**
- **Stelios Rotas**
- **Panagiotis Thivaios**

## Links

- Main app repo (Cassini-era): https://github.com/AlexTuring010/crowdless
- AI-Hackathon-winning rebuild (private): https://github.com/EXARTeo/Crowdless_App
- Crowdless project page: https://www.linkedin.com/company/crowdlessapp/
- AI Hackathon 2026 winners post: https://www.linkedin.com/posts/aihackathon2026-opentrack-innovationecosystem-ugcPost-7436487613802381312

## License

MIT — see [LICENSE](./LICENSE).
