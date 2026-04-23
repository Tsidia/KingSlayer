# Armello Combat Calculator

A small companion tool for [Armello](https://store.steampowered.com/app/290340/Armello/) that estimates the odds of every possible outcome of a fight before you commit to it. Designed to be kept open in a browser tab while you play, with steppers you can poke between turns.

No installs, builds, or servers are needed, just open `armello.html` in your browser.

<img width="1906" height="299" alt="image" src="https://github.com/user-attachments/assets/7fe236bc-c701-4623-964b-fc843541bc1a" />


## What it answers

Given the dice each side will roll, their health, their explosion caps, and any pre-locked hits or shields, it returns:

- **You win** - enemy dies, you survive
- **Enemy wins** - you die, enemy survives
- **Stalemate** - both survive
- **Mutual demise** - both die

Plus average damage dealt, average damage taken, total survival chance, and total kill chance.

Numbers come from a Monte Carlo simulation - 50,000 simulated battles per calculation, recomputed instantly whenever you nudge a value. The standard error sits around 0.2%, which is well below the precision anyone actually needs at the table.

<img width="1562" height="521" alt="image" src="https://github.com/user-attachments/assets/76ce02dd-f336-4ac9-852d-1c5aab14c6f8" />


## Modes

### Standard

The normal Armello die has six faces: worm, sword, shield, wyld, sun, and moon. The sun is a hit during the day and a miss at night; the moon does the opposite. Since exactly one of them is always a miss and the other is always a hit, the calculator collapses both into the dice math directly. Effectively each die is:

- 2/6 miss
- 2/6 hit
- 1/6 shield
- 1/6 wyld (a hit *and* an extra die - until that side's explosion cap is reached, after which wylds are just hits)

Damage is `max(0, hits − shields)` per side, with bonus hits and shields added in before that subtraction. Anyone whose damage taken meets or exceeds their HP dies.

### Slay the King

The King fight has its own rules:

- The **worm** rolls a shield for the King instead of a miss. (The wrong-time-of-day die is still a normal miss - only the worm specifically shields up.)
- The King **waits for the player to roll first**, then picks up every player miss as a bonus die for himself and rolls those alongside his own pool. Wyld explosions still apply on top, governed by his explosion cap.

Toggle between the two modes at the top of the page.

## Inputs

For each side:

- **Dice rolled**
- **Health**
- **Max explosions** (how many wylds can chain into extra dice before they revert to plain hits)
- **Bonus hits** - pre-locked sword symbols from cards, rings, terrain, etc.
- **Bonus shields** - same idea, for shields

Every field is a `−` / number / `+` stepper. You can type into the number directly or click the buttons.

<img width="1599" height="508" alt="image" src="https://github.com/user-attachments/assets/6637bc5d-3731-4b2c-9500-49d617d602d0" />


## Running it

Double-click `armello.html`, or open it from your browser's File menu. That's the whole setup. It runs entirely client-side; nothing leaves your machine.
