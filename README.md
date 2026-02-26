# Giran Insider Trading

A browser-based market tracker for **Lineage 2 Reborn** (C5 Chronicle). It logs prices you observe in player shops and applies basic statistical methods (EMA, z-scores, IQR filtering) to help you decide whether to buy, sell, hold, or craft. It also calculates crystallization value for equipment bundles and crafting profitability for material recipes.

All data stays in your browser's `localStorage`. Nothing is transmitted to any server. Your price history remains private, which means your observations cannot feed anyone else's trading decisions.

## Scope and limitations

This tool covers **D-grade and C-grade items only**. B/A/S-grade support does not exist yet, because I don't have a good understanding of that market (still learning). If you want to help me out with including those grades, send me a DM on Discord!

The trading signals (STRONG BUY, BUY, HOLD, SELL, STRONG SELL) are z-scores derived from your own logged data. They reflect where the latest price sits relative to a short-term moving average of prices *you* recorded. They do not predict future prices. Their quality depends entirely on how many observations you log and how representative those observations are.

The 440-item database and 32 crafting recipes are hard-coded from [lineage2wiki.org](https://lineage2wiki.org) C5 data. If the server's item stats differ from the wiki, the calculations here will be wrong.

## Quick start

Open the app at: **https://vkotzamanis.github.io/L2InsiderTrading/**

To test without entering real data, import the `demo.json` file included in this repo (History tab → Import JSON). To start fresh afterward, clear your browser's localStorage for this page.

## What it does

The app has six tabs.

### Log

Record a market observation. Pick an item from the database (or type a custom name), set the transaction type to BUY or SELL, enter the price in adena, choose a town, and hit Log. Prices accept shorthand: `1.5k` = 1,500 and `2.5kk` = 2,500,000. A checkbox toggles the display format across the entire app between full comma-separated numbers and compact k/kk notation.

### History

Browse, search, and filter every entry you have logged. You can delete individual rows, export your dataset as CSV, or use the JSON export/import system to back up and transfer data between devices. The import merges entries by ID, so duplicates are skipped automatically.

### Analytics

Build a watchlist of items you trade often. For each watched item the panel shows a mini stock chart with a 7-point EMA, the current z-score, and a trading signal. Outliers are flagged via IQR filtering so a single mistyped price does not distort your averages.

### Shots

A soulshot and spiritshot cost calculator for D-grade and C-grade. It computes the cheapest way to obtain crystals (player shop vs. NPC crystallization paths), then derives the per-unit crafting cost for each shot type. Enter the price you see in a player shop and the calculator tells you whether buying or crafting is cheaper, and by how much.

### Bargain

Evaluate equipment package deals. Search for items, add them to a list, enter the seller's asking price, and the calculator totals their crystallization value using your current best crystal cost. It shows net profit or loss so you can decide on the spot whether a bulk offer is worth taking.

### Crafting

A profitability calculator for 32 verified C5 crafting recipes. For every recipe, the app recursively resolves each ingredient to its cheapest source — your logged market prices, a sub-recipe's crafting cost, or a manual override you type in. It compares the total crafting cost against the average price buyers are paying, showing profit per batch and margin. Recipes with complete data sort to the top; incomplete ones show which prices are missing. Stale data (older than 7 days) is flagged with a red dot.

## How it works

The entire application is a single `index.html` file. It loads React 18 and Babel from a CDN, compiles JSX in the browser, and renders into a `<div id="root">`. There is no build step, no bundler, and no server. Persistent state lives in `localStorage` under four keys: `l2-market-v3`, `l2-shots-prices-v1`, `l2-analytics-watch-v1`, `l2-numfmt-v1`.

The item database (`ITEM_DB`) contains 440 D/C-grade tradeable items. Each entry stores the item name, grade, crystal yield, and equipment type. Crafting recipes, NPC crystallization paths, shot recipes, and NPC ore prices are hard-coded constants verified against C5 game data.

Key algorithms:

- **EMA**: α = 2/(N+1), N = 7.
- **Outlier rejection**: IQR method. Values below Q1 − 1.5·IQR or above Q3 + 1.5·IQR are excluded from averages.
- **Trading signals**: z-score of the latest price relative to the EMA, using the residual standard deviation of the price–EMA series.
- **Crafting cost resolution**: recursive depth-first search. For each ingredient it checks, in order: manual override → market sell-price average → sub-recipe crafting cost. It picks the cheapest path and propagates costs upward. A visited-set prevents infinite loops on circular references.

## Privacy

No server, no accounts, no tracking. All data is stored locally in your browser. Not even the author can see your data.

## Credits

Item database, crystal yields, and recipe data sourced from [lineage2wiki.org](https://lineage2wiki.org) (C5 Chronicle). Made by Vaxil with Claude Opus 4.6 · L2 Reborn Franz · 2026.
