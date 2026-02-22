# The Isofarian Guard 2E - Companion App

An unofficial companion web app for **The Isofarian Guard 2E** board game. Browse enemies, plan crafting routes, track resources, and look up market prices — all in a single offline-ready HTML file.

**[Live App](https://lincolnerickson.github.io/isofarian-guard-companion/)**

## Features

- **Enemies** — Full bestiary with stats, loot drops, and locations by chapter. Filter by star rating.
- **Armor & Weapons** — Crafting recipes with material requirements, costs, and prerequisites.
- **Accessories & Items** — Accessory recipes and effects.
- **Market** — Buy/sell prices across all 7 towns.
- **Ft. Istra Buildings** — Building upgrades, resource costs, and unlock requirements.
- **Speaking Stones** — Bonus effects and availability.
- **Material Finder** — Cross-reference any material: which enemies drop it, which recipes need it, where to buy it.
- **My Resources** — Track your collected materials, defeated enemies, and completed buildings. Persists in localStorage.
- **Route Planner** — Interactive map with 98 nodes and 179 edges. Select items to craft, pick a starting town, and get an optimized gathering route with step-by-step directions.

### Route Planner Details

- Canvas-rendered map with zoom/pan over the full game map
- BFS shortest-path + greedy nearest-source + 2-opt optimization
- Water edges (require Boat Dock building)
- Editor mode for adjusting node positions: drag nodes, shift+click to toggle edges, right-click to delete
- Export/import graph as JSON; save to localStorage

## Building

### Prerequisites

- Python 3.6+
- [openpyxl](https://pypi.org/project/openpyxl/)

```bash
pip install openpyxl
```

### Generate the app

```bash
python build_app.py
```

This reads `TIG_2E_Unofficial_Index_Companion_v2.xlsx` and produces:

- `isofarian_companion.html` — the complete app (single self-contained file)
- `index.html` — identical copy for GitHub Pages

Open either file in a browser. No server required.

## Project Structure

| File | Description |
|------|-------------|
| `build_app.py` | Build script — parses Excel data and generates the HTML app |
| `TIG_2E_Unofficial_Index_Companion_v2.xlsx` | Source data (7 sheets: bestiary, crafting, market, buildings, etc.) |
| `map-of-isofar.png` | Game map image (3000x4511 px), used by the route planner |
| `index.html` | Generated app (GitHub Pages entry point) |
| `isofarian_companion.html` | Generated app (primary output) |

## How It Works

1. `build_app.py` reads 7 Excel sheets with openpyxl
2. Parses enemies, armor/weapons, accessories, market prices, buildings, speaking stones, and prerequisite chains
3. Enriches map graph nodes with chapter, enemy, and resource metadata
4. Embeds everything as JSON inside a single HTML file with inline CSS and JavaScript
5. The browser app builds cross-reference indices (`materialToEnemies`, `materialToCraft`, `materialToMarket`) at load time

## Credits

- Game data spreadsheet originally created by [iNogle](https://boardgamegeek.com/profile/iNogle) on BoardGameGeek
- The Isofarian Guard is the property of its respective creators

This is an unofficial fan project.
