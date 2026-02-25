# 🎨 VISUAL TWEAKING CHEAT SHEET
# Open index.html in any text editor. Use Ctrl+H (Find & Replace).

## ─── COLORS (search → replace) ─────────────────────────────────────
#12100c   = page background (very dark brown)
#1a1710   = card background
#0f0d09   = input field background
#2a2418   = card borders
#3a3020   = tab borders / accents

#e8c55a   = GOLD (titles, prices, highlights)
#d4a843   = DARK GOLD (section titles, accents)
#d4c9a8   = LIGHT TAN (main body text)
#7a7464   = GRAY (labels, dimmed text)
#5a5448   = DARKER GRAY (very dim text)

#4ade80   = GREEN (BUY FOR, profit, good signals)
#c084fc   = PURPLE (SELL FOR)
#f87171   = RED (losses, bad signals)
#fbbf24   = YELLOW/AMBER (warnings, SELL signals)

## ─── TEXT & EMOJIS (find exact text) ────────────────────────────────
⚔ Giran Insider Trading     → change app title
L2 Reborn Franz, made by Vaxil with Claude Opus 4.6  → subtitle
📖 How to use:              → change to any emoji/text
📖 Market Dashboard         → analytics tab header
📖 How this works           → shots tab header
📊 Crystallization Paths    → section title
⚔ D-Grade Shots             → section title
💎 Equipment Bargain        → bargain title
🔨 Crafting Profitability   → crafting title
★ BEST                      → best recipe badge
⚒                           → craft path icon
🛒                           → buy path icon
⚡                           → override icon
✕                           → remove/close buttons

## ─── TAB NAMES ──────────────────────────────────────────────────────
Search for this line to change tab labels:
  ["log","Log"],["history","History"],["analytics","Analytics"],["shots","⚔ Shots"],["bargain","💎 Bargain"],["crafting","🔨 Crafting"]

## ─── FONT SIZES ─────────────────────────────────────────────────────
fontSize: 24    = biggest number displays
fontSize: 22    = stat counters
fontSize: 17    = shot batch totals
fontSize: 16    = latest price in analytics
fontSize: 15    = section titles, input text
fontSize: 14    = body text, buttons, inputs
fontSize: 13    = descriptions, tab labels
fontSize: 12    = labels, small stats
fontSize: 11    = badges, tiny labels

## ─── CARD LAYOUT ────────────────────────────────────────────────────
# Crafting grid (2 cards per row):
  gridTemplateColumns: "1fr 1fr"
  → change to "1fr 1fr 1fr" for 3 per row

# Analytics grid (4 charts per row):
  repeat(4, 1fr)
  → change to repeat(3, 1fr) for 3, or repeat(2, 1fr) for 2

# Container width for crafting/analytics:
  960
  → make it 1100 for wider, 800 for narrower

## ─── BORDER RADIUS (roundness) ──────────────────────────────────────
borderRadius: 10   = cards (rounder = higher number)
borderRadius: 8    = crafting cards, charts
borderRadius: 6    = inputs, buttons, small elements
borderRadius: 4    = badges, tiny elements

## ─── QUICK RECIPES ──────────────────────────────────────────────────

Want DARKER background?    Replace #12100c with #0a0908
Want LIGHTER cards?        Replace #1a1710 with #222018
Want BLUE instead of GOLD? Replace #e8c55a with #60a5fa
Want BIGGER fonts overall? Find fontSize: 13 → 14, fontSize: 14 → 15, etc.
Want MORE spacing?         Find gap: 10 → gap: 14, padding: 12 → padding: 16
