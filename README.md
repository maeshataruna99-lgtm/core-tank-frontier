# Core Tank Frontier

🎮 **Play now: https://core-tank-frontier.vercel.app/**

Roguelike survival tank 3D — browser game built with Three.js.

Survive endless waves of enemies in an isometric arena. After each wave,
draft 1 of 3 part cards to upgrade your tank (hull, tracks, turret, cannon,
engine, utility). Die, and the run ends — how far can you get?

## Play

- **Easiest:** open `index.html` directly in a browser
  (needs internet — Three.js loads from CDN).
- Best experienced on desktop/laptop with keyboard + mouse.

## Controls

| Input | Action |
|---|---|
| WASD / Arrows | Move (screen-relative) |
| Mouse | Aim turret |
| Hold Left Click | Fire |
| Space | Dash (requires Overdrive part) |
| M | Mute |

## How it works

- **Waves 1–9:** survive, clear all enemies, then draft a part card.
- **Wave 10:** boss fight — Dreadnought with 3 attack patterns.
- **Cards:** 17 parts across 6 slots, rarities Common → Legendary.
  Duplicates stack up to Lv 3 (Legendaries are unique). Reroll available.
- **Evolutions:** draft 1 dari 3 evolusi UNIK tiap wave 3/6/9 (boleh kumpulkan
  beberapa varian, masing-masing cuma bisa diambil sekali).
- **Pickups:** scrap (currency) and repair kits drop from enemies.

## Project layout

```
index.html          # the whole game (single file, no build step)
docs/breakdown.md   # game design breakdown
docs/planning.md    # project planning & roadmap
```

## Deploy

Static site — deployable as-is to Vercel, Netlify, or GitHub Pages.
No build step, no backend required.

## Roadmap

See [docs/planning.md](docs/planning.md).
