# FleetHub — Starsector Fleet Library

A static web app for building, sharing, and importing Starsector fleets — no backend required.

## Features

- **Fleet Builder** — Browse all vanilla ships, add them to your fleet, see stats update in real time
- **Fleet Codes** — Export your fleet as a compact shareable string that encodes name, author, and all ships
- **Import** — Paste any FleetHub code to instantly reconstruct and inspect a fleet
- **Zero backend** — Runs entirely client-side. Host on GitHub Pages or open `index.html` locally.

## Fleet Code Format

Fleet codes are self-contained strings using base64 + XOR obfuscation:

```
FH1_<base64payload>_<checksum>
```

The payload encodes: fleet name, author, description, objective, and ship list. No server needed — the code *is* the data.

## Running Locally

```
# Option 1: just open it
open index.html

# Option 2: local server (avoids fetch() CORS on some browsers)
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Deploying to GitHub Pages

1. Fork or clone this repo
2. Push to your GitHub account
3. Go to Settings → Pages → Source: `main` branch, root `/`
4. Done — your fleet library lives at `https://yourusername.github.io/fleethub/`

## Adding Community Fleets

Community fleets live in `data/fleets/community.json`. To submit yours:

1. Build your fleet in the app
2. Export as JSON
3. Add it to `data/fleets/community.json`
4. Submit a Pull Request

## File Structure

```
/index.html          — Single-page app (HTML + CSS + JS)
/data/
  ships.json         — Vanilla ship database
  factions.json      — Faction metadata
  fleets/
    community.json   — Community fleet library
```

## Adding Ships

Edit `data/ships.json`. Each ship needs:

```json
{
  "id": "unique_id",
  "name": "Ship Name",
  "faction": "Faction Name",
  "hull_size": "capital|cruiser|destroyer|frigate",
  "dp": 20,
  "fuel": 200,
  "cargo": 100,
  "crew": 500,
  "burn": 10,
  "supply_use": 15,
  "role": ["combat"],
  "description": "Short description."
}
```

## Roadmap

- [ ] Community fleet explorer (browse without importing)
- [ ] Fleet comparison side-by-side
- [ ] Officer assignment
- [ ] Mod support (user-supplied ship JSONs)
- [ ] Shareable URLs via URL hash encoding
- [ ] Vote / rating system (GitHub Issues integration)
