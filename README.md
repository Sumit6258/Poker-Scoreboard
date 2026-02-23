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


---

# 🃏 The Wonderfully Absurd Mathematics of Card Games

> *A README for people who suspected poker was secretly a math exam in disguise — and were right.*

---

## 🎴 The Deck Itself: A Universe in 52 Cards

A standard deck has **52 cards**. That sounds modest. It isn't.

The number of ways to shuffle a deck is **52 factorial** — written as 52! — which equals:

```
80,658,175,170,943,878,571,660,636,856,403,766,975,289,505,440,883,277,824,000,000,000,000
```

That's roughly **8 × 10⁶⁷**.

To put that in perspective:
- The number of atoms in the observable universe is estimated at ~10⁸⁰
- So a shuffled deck has *almost as many arrangements as there are atoms in the universe*
- **Every time you shuffle a deck properly, you are almost certainly creating an arrangement that has never existed before in all of human history — and never will again.**

---

## ♠ Texas Hold'em: The Staggering Possibilities

### Starting Hands

You're dealt 2 cards from 52. The number of possible starting hands is:

```
C(52,2) = 52! / (2! × 50!) = 1,326 unique two-card combinations
```

But because suits matter for strategy, there are **169 strategically distinct** starting hands:
- **13** pocket pairs (AA, KK, QQ... 22)
- **78** suited hands (AKs, AQs... 23s)
- **78** offsuit hands (AKo, AQo... 32o)

### The Full Board

In a game of Hold'em, 5 community cards are eventually dealt. The total number of unique 5-card boards from the remaining 50 cards:

```
C(50,5) = 2,118,760 possible boards
```

Combined with your 2 hole cards, the number of distinct 7-card combinations any one player can see:

```
C(52,7) = 133,784,560 possible 7-card deals
```

---

## 🤯 Hand Probabilities: The Full Breakdown

From a fresh 52-card deck, the number of unique **5-card hands** is:

```
C(52,5) = 2,598,960
```

Here's how they break down — including some numbers that will make you feel both humble and smug at the poker table:

| Hand | Combinations | Probability | Odds Against |
|------|-------------|-------------|--------------|
| Royal Flush | **4** | 0.000154% | 649,739 : 1 |
| Straight Flush | **36** | 0.00139% | 72,192 : 1 |
| Four of a Kind | **624** | 0.024% | 4,164 : 1 |
| Full House | **3,744** | 0.144% | 693 : 1 |
| Flush | **5,108** | 0.197% | 508 : 1 |
| Straight | **10,200** | 0.392% | 254 : 1 |
| Three of a Kind | **54,912** | 2.11% | 46.3 : 1 |
| Two Pair | **123,552** | 4.75% | 20.0 : 1 |
| One Pair | **1,098,240** | 42.26% | 1.37 : 1 |
| High Card | **1,302,540** | 50.12% | 0.995 : 1 |

> 🎯 **Fun fact:** You are more likely to be dealt a "nothing" (high card) hand than anything else. Over half of all 5-card deals are complete duds. Poker is largely a game of bluffing mediocrity.

---

## 😂 The Funny Numbers

### The Royal Flush Problem
There are only **4 possible Royal Flushes** in the entire universe of 2,598,960 hands. If you played one hand per second, non-stop, you'd expect to see a Royal Flush once every **~7.5 days**. Most casual players never see one in their lifetime. If you've seen one, you are statistically extraordinary. If you've seen two, consider buying a lottery ticket.

### Pocket Aces vs. Pocket Kings
Pocket Aces (AA) beat Pocket Kings (KK) approximately **82% of the time** in a heads-up pre-flop situation. The Kings win about 18% of the time. This remaining 18% is responsible for approximately **97% of all poker rage-quits**.

### The "Bad Beat" Math
Flopping a Royal Flush draw (holding two suited Broadway cards and flopping three of the remaining suited cards) has odds of roughly **1 in 19,600**. Yet somehow, someone at your table claims this happens to them constantly.

### All-In and a Coin Flip
Pocket Jacks vs. Ace-King offsuit (the classic "flip") is actually **57% vs. 43%** — not exactly a coin flip. JJ is a slight favorite. Knowing this won't make losing to an ace on the river feel any better.

---

## 🃏 Other Card Games: Also Mathematically Wild

### Rummy
A standard 13-card rummy hand is drawn from 52 cards:

```
C(52,13) = 635,013,559,600 possible hands
```

That's **635 billion** unique starting hands. The chance of any two players ever receiving identical hands across all of history is effectively zero.

### Teen Patti (3 Patti)
Dealt 3 cards from 52:

```
C(52,3) = 22,100 possible three-card hands
```

The rarest hand — a **Trail (Three of a Kind)** — has only 52 combinations (13 ranks × 4 card combinations). Probability: **0.24%**, or about 1 in 425.

The most common hand — **High Card** — accounts for **16,440 combinations** (~74% of all hands). Teen Patti is mostly high-card poker with occasional drama.

### Bridge
Bridge deals 13 cards to each of 4 players from a 52-card deck. The number of ways to deal the entire deck:

```
52! / (13! × 13! × 13! × 13!) = 53,644,737,765,488,792,839,237,440,000
```

That's about **5.36 × 10²⁸** possible deals. The total number of Bridge deals ever played in human history is estimated at around 10¹⁷ — meaning the vast majority of possible Bridge deals have **never been seen and likely never will be**.

### Spades
Spades uses all 52 cards dealt to 4 players (13 each). Same deal count as Bridge: ~5.36 × 10²⁸ possible arrangements.

---

## 🧠 Counterintuitive Poker Facts

### The Monty Hall Problem of Poker
If you hold pocket Aces and your opponent holds pocket Kings, and the flop comes K-K-2 (giving them four Kings)... you still technically have "outs." Specifically, you need the board to pair and your kicker to play. Spoiler: it won't. But mathematically, your hand isn't completely dead until the river.

### More Cards ≠ Better Odds
In 7-card stud, players receive 7 cards to make their best 5. Having 7 cards doesn't mean you'll get good hands more often — it means the distribution shifts slightly upward, but **most hands are still one pair or worse**.

### The Paradox of Tight Play
Statistically, the best starting hand strategy (playing only top ~15% of hands) means you fold **85% of the time before seeing a flop**. Professional poker at the top level involves mostly... not playing. You're paying to watch other people make mistakes.

### Suited Cards Aren't That Special
The probability boost from being suited (vs. offsuit) for making a flush is only about **3–4 percentage points** in Hold'em. Beginners dramatically overvalue suited cards. "It's suited!" is the poker equivalent of "It's organic!" — technically meaningful, but probably not changing the outcome.

---

## 🌍 Scale of Possibility: The Big Picture

| Statistic | Number |
|-----------|--------|
| Unique 52-card shuffles | ~8 × 10⁶⁷ |
| Atoms in observable universe | ~10⁸⁰ |
| Unique 5-card hands | 2,598,960 |
| Unique 7-card Hold'em deals | 133,784,560 |
| Unique 13-card Bridge deals (per player) | 635,013,559,600 |
| Unique full Bridge deals (all 4 players) | ~5.36 × 10²⁸ |
| Probability of flopping a Royal Flush draw | 1 in ~19,600 |
| Probability of flopping quads (with a pocket pair) | ~1 in 407 |
| Probability of hitting a gut-shot straight draw on the river | ~8.7% |
| Hands played in human poker history (est.) | ~10¹⁷ |

---

## 😄 Philosophical Implications

1. **Every poker hand is unique.** With ~133 million possible 7-card deals, and accounting for player count, bet sizing, and action sequences — no two poker hands in history have been identical in every dimension.

2. **Luck runs out... very slowly.** The "long run" in poker is approximately 100,000+ hands for statistical variance to smooth out. Most home game players will never play that many hands in their lifetime. Which means variance (luck) is always a significant factor. Which explains why your uncle keeps winning.

3. **The best hand pre-flop loses often enough to keep everyone playing.** Pocket Aces win only ~85% of the time heads-up, and less against multiple opponents. This ~15% losing rate is what makes poker a game rather than a chore.

4. **The universe is generous with randomness.** In any serious poker career spanning millions of hands, a player will experience streaks and droughts that seem statistically impossible — and yet are perfectly predicted by variance. The math is not broken. It just feels broken.

---

## 🏆 Quick Reference: Memorable Odds

```
Royal Flush:        1 in 649,740   — rarer than being struck by lightning (twice)
Straight Flush:     1 in 72,193    — rarer than finding a four-leaf clover
Four of a Kind:     1 in 4,165     — about as likely as flipping heads 12 times in a row
Full House:         1 in 694       — surprisingly common, yet still special
Any pair or better: ~50%           — you'll have something to work with half the time
Flopping a set:     ~11.8%         — if you hold a pocket pair
Gutshot straight:   ~8.5% per card — never chase it. (Everyone chases it.)
Backdoor flush:     ~4% by river   — do not build your strategy around this
```

---

## 🔢 The Code Behind This App

This scoreboard tracks your real-world poker sessions so that, over time, you can observe your own statistical journey through the ~133 million possible Hold'em deals. Will your results converge on the mathematically expected values?

Probably not in the sessions you actually track. But the math says: eventually, yes.

That's the beautiful, maddening, wonderful promise of probability.

---

*Built with ♠♥♦♣ and a deep respect for combinatorics.*
*May your Royal Flushes be plentiful and your bad beats forgettable.*

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
