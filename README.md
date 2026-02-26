# Giran Insider Trading

A browser-based market tracker for **Lineage 2 Reborn** (C5 Chronicle). It logs prices, detects bargains, calculates crafting profitability, and tells you whether to buy or craft your soulshots — all without a server. Every byte of data stays in your browser's localStorage.

## How to use:
Open the github page below:
https://vkotzamanis.github.io/L2InsiderTrading/
Import your own data or load the sample .json file  inlcuded in this repo and play around.
## What it does

The app has six tabs. Each solves a different problem.

### Log

Record a market observation. Pick an item from the 440-item D/C-grade database (or type a custom name), set the transaction type to BUY or SELL, enter the price in adena, choose a town, and hit Log. Prices accept shorthand: `1.5k` = 1,500 and `2.5kk` = 2,500,000. A checkbox toggles the display format across the entire app between full comma-separated numbers and compact k/kk notation.

### History

Browse, search, and filter every entry you have logged. Entries display with date, time, item, type, price, and location. You can delete individual rows, export your full dataset as CSV, or use the JSON export/import system to back up and transfer data between devices.

### Analytics

Build a personal watchlist of items you trade often. For each watched item the panel shows a mini stock chart with a 7-point Exponential Moving Average (EMA), the current z-score relative to that EMA, and a signal: STRONG BUY, BUY, HOLD, SELL, or STRONG SELL. Outliers are flagged via IQR filtering so a single mistyped price does not distort your averages.

### Shots

A soulshot and spiritshot cost calculator for D-grade and C-grade. It computes the cheapest way to obtain crystals (player shop vs. NPC crystallization paths), then derives the per-unit crafting cost for each shot type. Enter the price you see in a player shop and the calculator tells you whether buying or crafting is cheaper, and by how much.

### Bargain

Evaluate package deals. Search for items from the database, add them to a list, enter the seller's asking price, and the calculator totals their crystallization value using your current best crystal prices. It shows net profit or loss so you can decide on the spot whether a bulk offer is worth taking.

### Crafting

A profitability engine for 32 verified C5 crafting recipes. For every recipe, the app recursively resolves each ingredient to its cheapest source — your logged market prices, a sub-recipe's crafting cost, or a manual override you type in. It then compares the total crafting cost against the average price buyers are paying, showing profit per batch and profit margin. Recipes with complete data sort to the top; incomplete ones appear below with clear indicators of which prices are missing. Stale data (older than 7 days) is flagged with a red dot.

## How it works

The entire application is a single `index.html` file. It loads React 18 and Babel from a CDN, compiles JSX in the browser, and renders into a `<div id="root">`. There is no build step, no bundler, and no server. All persistent state lives in `localStorage` under a handful of keys (`l2-market-v3`, `l2-shots-prices-v1`, `l2-analytics-watch-v1`, `l2-numfmt-v1`).

The item database (`ITEM_DB`) contains 440 D-grade and C-grade tradeable items scraped from [lineage2wiki.org](https://lineage2wiki.org). Each entry stores the item name, grade, crystal yield, and equipment type. Crafting recipes, NPC crystallization paths, shot recipes, and NPC ore prices are all hard-coded constants verified against the C5 game data.

Key algorithms:

- **EMA calculation** uses the standard formula α = 2/(N+1) with N = 7.
- **Outlier rejection** uses the interquartile range (IQR) method: values below Q1 − 1.5·IQR or above Q3 + 1.5·IQR are excluded from averages.
- **Trading signals** are z-scores of the latest price relative to the EMA, computed against the residual standard deviation of the price–EMA series.
- **Crafting cost resolution** is a recursive depth-first search. For each ingredient, it checks (in order): manual override → market sell-price average → sub-recipe crafting cost. It picks the cheapest path and propagates costs upward. A visited-set prevents infinite loops on circular references.

## How to use it

1. Clone or download this repo.
2. Open `index.html` in any modern browser. No installation required.
3. Start logging prices you observe in the Giran (or any town) private shops.
4. As your dataset grows, the Analytics, Shots, Bargain, and Crafting tabs become increasingly useful.

To move your data to another device, go to **History → Export JSON**. On the new device, use **Import JSON**. The import merges entries by ID so duplicates are skipped automatically.

## Testing with demo data

A `demo.json` file is included in this repository. It contains a sample dataset of market entries you can import to crash-test every feature without logging real prices first. To use it:

1. Open the app in your browser.
2. Go to the **History** tab.
3. Click the **Import JSON** button and select `demo.json`.
4. All tabs will now populate with data. Browse Analytics charts, check Shots verdicts, evaluate a Bargain deal, and review Crafting profitability.

To start fresh afterward, clear your browser's localStorage for this page.

## Privacy

No server, no accounts, no tracking. All data is stored locally in your browser. Not even the author can see your data.

## Credits

Item database, crystal yields, and recipe data sourced from [lineage2wiki.org](https://lineage2wiki.org) (C5 Chronicle). Made by Vaxil with Claude Opus 4.6 · L2 Reborn Franz · 2026.
