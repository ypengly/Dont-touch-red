# DON'T TOUCH THE RED 🔴

A polished, single-file browser arcade survival game. Avoid anything red, collect coins, and survive as long as you can while random chaos events keep things interesting.

## Contents

```
dont-touch-red/
├── dont-touch-red.html   ← the entire game (open this file)
└── README.md             ← this file
```

There are no other dependencies, build steps, or external assets — everything (graphics, sound, logic) is generated in a single self-contained HTML file.

## How to run it

1. Unzip the archive.
2. Double-click `dont-touch-red.html` (or open it from your browser with `File → Open`).
3. Play. That's it — no server, no install, no internet connection required.

It also works fine if you drop the file onto a static web host (Netlify, GitHub Pages, a plain Apache/nginx folder, etc.) — just upload `dont-touch-red.html`.

## Controls

| Input | Action |
|---|---|
| `W A S D` or Arrow Keys | Move |
| On-screen joystick (auto-shown on touch devices) | Move |
| `Esc` or the ⏸ button | Pause / Resume |

## Gameplay overview

- **Objective:** Survive as long as possible. Score climbs continuously the longer you're alive, plus bonus points for coins.
- **Lives:** You start with 3 hearts (1 in Hard Mode). Touching anything red costs a heart and gives you a brief invulnerability window (flashing sprite) so you can escape.
- **Coins:** Yellow coins spawn around the arena. Collecting one adds to your score and to your permanent coin balance (spendable in the Shop, kept between runs).
- **Difficulty:** Ramps up automatically over time — hazards spawn faster and move quicker the longer a run goes.

## Random events

Every 15–28 seconds (more frequently as difficulty rises) a random event fires, with an on-screen "⚠ EVENT NAME!" banner and a sound cue:

- **Falling Bombs** — a volley of red bombs drops from the top of the arena.
- **Laser Walls** — full-width/height red laser beams sweep back and forth.
- **Shrinking Arena** — the playable area temporarily contracts.
- **Red Enemies Spawning** — bouncing red enemies roam the arena for a while.
- **Reverse Controls** — your movement inputs are inverted.
- **Low Gravity** — a floaty movement-speed modifier.
- **Speed Boost** — a temporary speed multiplier (helps you escape, but overshooting is easy).
- **Giant Danger Zone** — a red zone grows from a point and lingers.
- **Multiple Hazards** — a "chaos" event that fires several hazard types at once.

Each event has its own duration and automatically reverts (controls, gravity, arena size, etc. return to normal) when it ends.

## Game modes

Pick a mode from the main menu before pressing Play:

- **Classic Survival** — standard 3 lives, standard difficulty ramp.
- **Endless Chaos** — same core rules; events and hazards are the main draw for repeat runs.
- **Time Challenge** — a fixed 90-second run; the goal is maximum score before time's up.
- **Hard Mode** — 1 life only and a steeper starting difficulty curve for experienced players.

## Progression, shop & cosmetics

- Coins earned during runs persist between sessions (saved to your browser's local storage).
- Open **Character** from the main menu to equip any skin you've unlocked.
- Open **Shop** to spend coins on additional character skins and cosmetic trail effects.
- Nothing purchased is pay-to-win — cosmetics only, all gameplay-affecting items are available to everyone from the start.

## UI & game states

The game moves through four clean states: **Menu → Playing → Paused → Game Over**, each with its own screen and no dead ends:

- **Menu:** Play, Game Mode, Character, Shop, Settings, and your current High Score / Coin balance.
- **In-game HUD:** live score, survival time, coins collected this run, remaining hearts, and a pause button. Event banners appear at the top-center when a random event triggers.
- **Pause screen:** Resume or return to the Main Menu — the run state is preserved while paused.
- **Game Over screen:** final score, survival time, coins collected, your all-time best score, a "New Record!" callout when you beat it, and Retry / Main Menu buttons.

## Audio

All music and sound effects are generated live with the Web Audio API — there are no external audio files to load, so the game works completely offline. Distinct cues play for coin pickups, taking damage, dying, event triggers, and button presses, plus a light looping background melody. Toggle **Music** and **Sound Effects** independently from Settings; your choice is remembered.

## Saved data

The game saves the following to your browser's `localStorage` (key: `dttr_save_v1`) — nothing is sent anywhere:

- High score
- Coin balance
- Unlocked skins & trails and your currently selected ones
- Music / SFX on-off preference
- Whether you've seen the first-time tutorial

To fully reset your progress, clear your browser's site data for the page (or open it in a private/incognito window).

## Mobile & responsive support

- The canvas scales to fit any screen size while preserving its aspect ratio.
- A touch joystick automatically appears on touch-capable devices in place of the keyboard hint.
- Layout respects device safe areas (notches / home indicators) on modern phones.

## Known simplifications

This build focuses on a fully playable, polished core experience. A couple of items from the original wishlist are intentionally simplified for this version, and would be natural next additions:

- **Rotating arena** and **disappearing floor tiles** are not yet implemented as standalone events (the other nine events are fully implemented).
- Cosmetic **trails** and **death effects** are currently purchasable shop items with basic visuals rather than fully unique animated effects per item.

If you'd like either of those built out, or additional skins/modes added, just ask.

## Customizing / extending the code

Everything lives in `dont-touch-red.html`:

- **CSS** (`<style>` block) controls all visual styling and is CSS-variable-driven (see `:root`) if you want to reskin colors quickly.
- **JavaScript** (`<script>` block) is organized into clearly commented sections: persistence, audio, skins/shop, navigation, input, game state, hazards, random events, the update/render loop, and pause/end handling.
- To add a new random event, add an entry to the `EVENTS` array with a `name`, `fn` (what happens when it starts), `dur` (seconds), and optional `end` (cleanup when it finishes).
- To add a new hazard type, add a `spawnX()` function and a matching branch in both the `update()` collision loop and the `render()` drawing loop.

Enjoy — and good luck not touching the red.
