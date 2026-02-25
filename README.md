# ⚔ Giran Insider Trading

**L2 Reborn Franz — Market Price Intelligence**

A self-contained market tracker for Lineage 2 Classic (C5 Reborn). Built by **Vaxil** with Claude Opus 4.6.

## Features

- **📋 Log** — Record SELL FOR / BUY FOR prices from player shops. Accepts `k` (×1,000) and `kk` (×1,000,000).
- **📜 History** — Browse all logged entries, delete mistakes, export to CSV.
- **📊 Analytics** — Per-item stock-market charts. Green = above avg (SELL), Red = below avg (BUY). Persistent watchlist.
- **⚔ Shots Calculator** — Crystal D/C cost paths, soulshot/spiritshot/BSPS craft vs buy analysis with cascading costs.
- **💎 Bargain Calculator** — Check if buying D/C equipment to crystallize is profitable. 440-item database.
- **🔨 Crafting** — 32 verified C5 recipes with recursive cost resolver. Finds cheapest path (craft vs buy) for every ingredient.

## Privacy

**All data is stored locally in your browser** (`localStorage`). Nothing is sent to any server. Each person builds their own database.

## Deploy to GitHub Pages

1. Fork or clone this repo
2. Go to **Settings → Pages**
3. Set source to `main` branch, root folder
4. Your site is live at `https://yourusername.github.io/repo-name/`

That's it — just one `index.html` file, no build step needed.

## Tech

Single HTML file. React 18 via CDN + Babel standalone. No dependencies, no build tools, no server.
