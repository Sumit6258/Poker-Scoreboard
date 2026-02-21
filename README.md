#  ♠ Card Scoreboard Pro v2

A fully-featured, mobile-first card game scoreboard that runs entirely in a single HTML file — no installs, no dependencies, no server. Open it in any browser and play.

![Poker Scoreboard](https://img.shields.io/badge/HTML-Single%20File-orange?style=flat-square&logo=html5)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Mobile Ready](https://img.shields.io/badge/Mobile-First-blue?style=flat-square)
![No Dependencies](https://img.shields.io/badge/Dependencies-None-brightgreen?style=flat-square)

---

## 🎮 Live Demo

> **[▶ Play it live on GitHub Pages](https://sumit6258.github.io/Poker-Scoreboard/)**
>


---

## What It Does

Track multi-player card games across a configured number of rounds. Poker mode has full betting logic (Call, Raise, MAX All-In, Fold) with a per-round chip budget system. Four other games use manual score entry per round. Every round is logged, profit/loss is tracked per player, and a Final Results screen shows the complete match breakdown when the last round ends.

---

## Getting Started

1. Open `index.html` in any modern browser
2. Select your game mode from the top bar
3. Click **⚙️ Lock In Match** — enter starting chips and total rounds
4. Add 2–6 players
5. Hit **▶ Start Round** and play

---

## Match Configuration

Before any round can begin, you set two values:

| Field | Description |
|---|---|
| **Starting Chips** | How many chips each player begins with (min 100) |
| **Total Rounds** | How many rounds the match will last (min 1) |

From these two numbers, the app calculates:

```
Max Bet Per Round = Starting Chips ÷ Total Rounds
```

**Example:** 1000 chips, 10 rounds → each player can bet at most **100 chips per round**. This budget resets every round regardless of wins or losses. A live preview shows the max-per-round calculation as you type.

---

## Poker Mode — Betting Actions

### Call
Match the current highest bet. The difference between the highest bet and your current bet is deducted from your chips and added to the pot. If you cannot cover the full amount within your round budget, you go all-in for whatever you have left.

### Raise
Set a new highest bet. Enter an amount in the raise field — the new highest bet becomes `current highest + your raise`. All other players must at least call this new amount. Raises are capped by your remaining round budget.

### MAX (All-In)
Bet your **entire remaining round budget** in one action.

- If you've already bet 10 out of your 100-chip budget, MAX puts in the remaining 90
- Once **any** player uses MAX, the round enters MAX mode: every other active player must either **MAX** or **Fold** — no partial bets or raises allowed
- The MAX button pulses red; a red banner appears across the player grid when MAX mode is active

**Example with 4 players, 1000 chips, 10 rounds (100 max/round):**
- Player A raises by 10 → 90 budget remaining
- Player A then MAXes → remaining 90 go into pot → Player A is all-in
- Players B, C, D now see only MAX or Fold

### Fold
Surrender your hand. Chips already in the pot are forfeited. You automatically re-enter next round. A confirmation prompt appears before the fold is registered (can be disabled in Settings).

---

## Round Flow

```
Configure Match → Add Players → Start Round → Players Act → Award Pot → Next Round
```

1. **Start Round** — snapshots each player's chip count for P/L accounting, resets bets and budgets, re-activates folded players
2. **Players act** — Call, Raise, MAX, or Fold in any order
3. **Award Pot** — select the winner from the dropdown and click Award
4. **Repeat** until the final round completes, then Final Results opens automatically

If all but one player folds, the pot is auto-awarded to the last standing player after a 2-second delay.

---

## Profit / Loss Accounting

Every round, the app records each player's chip count before and after:

```
Delta = End Chips − Start Chips
```

- Positive delta → added to Total Won
- Negative delta → added to Total Lost
- Net P/L = Total Won − Total Lost

This is shown live on every player card, in the Rankings table, on the Analytics page, and in Final Results.

---

## Leaderboard

The Rankings table shows a full per-player breakdown:

| Column | Description |
|---|---|
| Chips | Current chip count |
| Wins | Number of rounds won |
| Won Rounds | Which round numbers they won |
| Losses | Number of rounds lost |
| Lost Rounds | Which round numbers they lost |
| Folds | Total times folded |
| Folded Rounds | Which round numbers they folded |
| +Won | Total chips gained across all rounds |
| −Lost | Total chips lost across all rounds |
| Net P/L | Won minus Lost |

Sorted by Net P/L by default. Switch between **Session** and **All Time** views.

---

## Final Results

After the last round, the Final Results screen shows automatically:

- **Champion card** — top player by net profit, with final chips, rounds won, and net P/L
- **Full standings table** — every player with all stats including which rounds they won, lost, and folded
- **Highlights** — Champion, Biggest Loser, Most Folds, Biggest Single Pot
- **Match summary** — total rounds, game mode, max per round

From here you can **Play Again** (same players, chips reset) or **New Match** (full reset).

---

## Other Game Modes

Rummy, Spades, Teen Patti, and Bridge use manual score entry. Each round, enter each player's score and click **Submit Round Scores**. The same P/L accounting, leaderboard, history, and analytics apply.

---

## Pages

| Page | Contents |
|---|---|
| 🃏 Game | Play screen — game selector, config, player cards, rankings |
| 📜 History | Round-by-round log with chip deltas, export/clear |
| 📊 Stats | Bar charts, P/L breakdown table, highlights, session stats |
| ⚙️ Settings | Theme, preferences, match reconfiguration, data management |

The **📖 Rules** and **🃏 Hands** buttons float above the nav bar on every page.

---

## Player Profiles

Tap any player avatar to open their profile:

- Full stat grid: chips, wins, losses, win rate, folds, net P/L, total won, total lost, biggest pot
- Which specific rounds they won, lost, and folded
- Achievement badges (locked/unlocked)
- Option to reset that player's stats

---

## Achievements

| Badge | Unlock Condition |
|---|---|
| 🥇 First Win | Win your first round |
| 🔥 On Fire | Win 3 rounds in a row |
| 🌋 Unstoppable | Win 5 rounds in a row |
| 💰 5K Club | Accumulate 5,000+ chips |
| 📈 Aggressor | Raise 5+ times in a session |
| 🔥 All-In King | Use MAX 3+ times |
| 🛡️ Survivor | Win a round without having ever folded |
| 🎯 Big Pot | Win a pot of 500+ chips |

---

## Settings

| Setting | Default | Description |
|---|---|---|
| Theme | Dark Poker | Dark Poker / Neon Casino / Light |
| Sound Effects | On | Web Audio tones for chip, raise, fold, win |
| Confirm Before Fold | On | Prompt before registering a fold |
| Winner Celebration | On | Confetti animation on round win |
| Highlight Active Player | On | Green border on current turn |

---

## Undo

The **↩ Undo** button reverts the last action, including MAX triggered state. Up to 15 steps per round. Resets between rounds.

---

## Data Persistence

All state saves automatically to `localStorage` after every action. Refreshing or closing the browser restores the full match exactly as it was. Export the full session as a `.json` file at any time from the History page or Settings.

---

## Edge Cases

- **Bankrupt player** (0 chips) — auto-sits out; re-enters when chips are restored
- **All but one folds** — pot auto-awarded after 2 seconds
- **Call with insufficient budget** — player goes all-in for whatever they can afford
- **MAX with 0 remaining budget** — button disabled
- **Remove player during round** — blocked with error
- **Duplicate player names** — rejected on add
- **MAX triggered** — Call and Raise disabled; only MAX and Fold shown
- **Match complete** — all betting locked; Final Results re-openable

---

## Technical

| Property | Value |
|---|---|
| File count | 1 (single `index.html`) |
| Dependencies | None |
| Frameworks | None — vanilla JS, CSS, HTML |
| Storage | `localStorage` (key: `cgsb_v4`) |
| Browser support | Any modern browser |
| File size | ~115 KB |
| Lines | ~2,450 |

## 📄 License

MIT License — free to use, modify and distribute.

---

## 🙏 Contributing

1. Fork the repo
2. Make your changes to `index.html`
3. Open a Pull Request

Please keep everything in the single file — no build tools, no dependencies.

---

*Built with ♠ pure HTML, CSS & JavaScript — no frameworks, no libraries, no nonsense.*
