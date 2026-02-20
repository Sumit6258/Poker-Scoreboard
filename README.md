# ♠ Poker Scoreboard & Ranking System

A fully offline, mobile-first **Poker Chip & Score Manager** built as a single `index.html` file — no frameworks, no CDN, no build step required.

![Poker Scoreboard](https://img.shields.io/badge/HTML-Single%20File-orange?style=flat-square&logo=html5)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Mobile Ready](https://img.shields.io/badge/Mobile-First-blue?style=flat-square)
![No Dependencies](https://img.shields.io/badge/Dependencies-None-brightgreen?style=flat-square)

---

## 🎮 Live Demo

> **[▶ Play it live on GitHub Pages](https://YOUR-USERNAME.github.io/poker-scoreboard/)**
>
> *(Replace `YOUR-USERNAME` with your actual GitHub username after deployment)*

---

## 📸 Features at a Glance

| Feature | Description |
|---|---|
| 👥 **Player Management** | Add up to 6 players with custom chip counts |
| 📞 **Call / 📈 Raise / 🏳️ Fold** | Core poker actions with full chip math |
| 🪙 **Live Pot Tracker** | Animated pot display updates on every action |
| 🏆 **Rankings Board** | Auto-sorted leaderboard by score then chips |
| 🃏 **Hand Rankings Panel** | Visual playing card reference for all 10 hands |
| 📖 **Game Rules** | In-app rules guide — great for beginners |
| 🎰 **Round Counter** | Tracks how many rounds have been played |
| 📱 **Mobile-First** | Designed for phones — pass around the table! |
| ✨ **Micro-animations** | Card pulses, pot bumps, winner glow, ripples |
| 🌙 **Dark Casino Theme** | Premium glassmorphism dark UI |

---

## 🚀 Getting Started

### Option 1 — Open Directly (Zero Setup)

```bash
# Clone the repo
git clone https://github.com/YOUR-USERNAME/poker-scoreboard.git

# Open the file in any browser
open index.html
```

No server needed. No `npm install`. Just open the file.

---

### Option 2 — Host on GitHub Pages

1. **Fork or push** this repo to your GitHub account
2. Go to your repo → **Settings** → **Pages**
3. Under *Branch*, select `main` (or `master`) and folder `/root`
4. Click **Save**
5. Wait ~60 seconds, then visit:
   ```
   https://YOUR-USERNAME.github.io/poker-scoreboard/
   ```

That's it — live on the internet for free! ✅

---

## 🃏 How to Play

### Setup
1. Enter player names and chip amounts, click **＋ Add Player** (up to 6 players)
2. Click **▶ Start Round** to begin a hand

### Each Player's Turn
| Action | What Happens |
|---|---|
| **Call** | Matches the current highest bet; chips deducted, pot increased |
| **Raise** | Enter an amount → new bet = highest bet + raise; becomes new high |
| **Fold** | Player sits out until next round; their pot contribution is lost |

### Ending a Round
- Select the winner from the dropdown and click **🏆 Award Pot**
- Winner's chips increase by the pot total
- Winner's **Score** increases by the same amount (score never decreases)
- Rankings update automatically

### Scoring
- **Chips** = current wallet (fluctuates each round)
- **Score** = lifetime total of all pots won (only goes up)
- Leaderboard sorts by Score → Chips as tiebreaker

---

## 📁 File Structure

```
poker-scoreboard/
├── index.html      ← Entire app (HTML + CSS + JS, single file)
└── README.md       ← This file
```

Everything is embedded in `index.html`:
- ✅ All CSS (including animations, glassmorphism, responsive grid)
- ✅ All JavaScript (game logic, state management, rendering)
- ✅ Hand rankings data (all 10 hands with real card examples)
- ✅ Game rules content
- ✅ Toast notifications
- ✅ Ripple effects

---

## 🎨 UI Highlights

- **Glassmorphism cards** with `backdrop-filter: blur`
- **Premium gradient buttons** — Call (blue), Raise (gold), Fold (red), Start (green)
- **Ripple click feedback** on all buttons
- **Animated pot counter** bumps on every chip movement
- **Gold glow pulse** on the current highest bettor's card
- **Winner flash animation** after awarding the pot
- **Collapsible leaderboard** for mobile screen space
- **Two floating action buttons** — Hand Rankings 🃏 and Game Rules 📖
- **Bottom sheet modals** with spring easing animation

---

## 🧠 Technical Notes

### State Management
```js
// Core state
let players    = [];   // Array of player objects
let pot        = 0;    // Current round pot
let highestBet = 0;    // Highest bet this round
let roundNumber= 0;    // Round counter

// Player object shape
{
  id,          // Unique auto-increment ID
  name,        // Display name
  chips,       // Current chip count
  currentBet,  // Bet placed this round
  score,       // Cumulative lifetime score
  folded       // Boolean — folded this round?
}
```

### Key Functions
| Function | Purpose |
|---|---|
| `addPlayer()` | Validate + push new player |
| `startRound()` | Reset bets, re-activate players, increment round |
| `callPlayer(id)` | Match highest bet; handle all-in edge case |
| `raisePlayer(id)` | Raise above highest bet; update `highestBet` |
| `foldPlayer(id)` | Mark player folded |
| `endRound()` | Award pot to winner; update score |
| `renderPlayers()` | Re-render all player cards to DOM |
| `updateLeaderboard()` | Sort + re-render rankings table |

### Bet Formula
```
callAmount  = highestBet - player.currentBet
newBet      = highestBet + raiseAmount
chipsNeeded = newBet - player.currentBet
pot        += chipsNeeded
```

---

## 📱 Browser Support

Works in all modern browsers:

| Browser | Support |
|---|---|
| Chrome / Edge | ✅ Full |
| Firefox | ✅ Full |
| Safari (iOS) | ✅ Full |
| Samsung Internet | ✅ Full |

---

## 🔧 Customisation

Want to tweak the defaults? Edit these values in `index.html`:

```js
// Default chip count shown in the input
<input ... value="1000" ...>

// Maximum players
if (players.length >= 6) { ... }

// Toast display duration (ms)
}, 2800);
```

---

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
