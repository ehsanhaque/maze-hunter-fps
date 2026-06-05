# Maze Hunter — A 3D FPS Built on a Pac-Man-Style Maze

A single-file, browser-based **3D first-person shooter** set inside a classic
arcade-style maze. Wander a brick labyrinth, get hunted by glowing wraiths that
actually path-find through the corridors, grab power orbs to flip the hunt around,
and trigger timed elite waves with their own soundtrack.

> **Built with [Claude Code](https://claude.com/claude-code).** The entire game —
> engine, AI, audio, and HUD — was designed and written in collaboration with
> Anthropic's Claude Code.

> ⚠️ **Demo / experimental project — not affiliated with or endorsed by any rights
> holder.** This is a non-commercial, educational tech demo exploring 3D rendering,
> enemy AI, and synthesized audio in the browser. It is *inspired by* classic
> maze-arcade mechanics but uses no original assets, art, audio, characters, or
> trademarks from any existing game. All geometry, textures, and sound are
> generated procedurally at runtime. "Pac-Man" and any related marks are the
> property of their respective owners; this project is not associated with them in
> any way. Provided as-is for learning and demonstration purposes only.

---

## Play it

It's a **single self-contained HTML file** — no build step, no install.

1. Open `index.html` in a modern desktop browser (Chrome/Edge/Firefox).
2. Click to lock the mouse and start.

**Requirements:** an internet connection (Three.js is loaded from a CDN) and a
click to begin (browser audio only starts after a user gesture). For fully offline
play, vendor Three.js locally and point the importmap at it.

## Controls

| Input | Action |
|-------|--------|
| **WASD** | Move |
| **Mouse** | Look |
| **Shift** | Sprint |
| **Left click** | Fire (hold for automatic weapons) |
| **R** | Reload |
| **M** | Cycle minimap (small → large → hidden) |
| **Esc** | Release mouse / pause |

## Features

**World & rendering**
- The maze grid is built into a 3D brick labyrinth — floor and ceiling planes plus
  walls as a single `InstancedMesh`.
- Procedurally generated canvas textures (brick walls, gritty floor) — zero external
  art. PBR `MeshStandardMaterial` throughout.
- Bright, moody lighting: ambient + hemisphere fill, a directional light, a player
  flashlight spotlight with soft shadows, flickering colored corridor lights, and
  thin exponential fog.

**Enemy AI**
- Hunters are billboarded glowing-wraith sprites that use **real maze pathfinding** —
  a BFS flow field recomputed from the player's cell several times a second; each
  hunter follows the descending-distance corridor.
- Perception: hunters **patrol** (slow, dim) until they get line of sight or hear
  you nearby, then **chase** (red, full speed) and keep pursuing for a few seconds
  after losing sight.

**Weapons** — config-driven: **Pistol**, **Machine Gun**, and **Laser Rifle**
(with a visible beam), each with its own fire rate, damage, magazine, recoil, and
muzzle color. Low-poly viewmodel with muzzle flash and recoil.

**Power orbs → Frenzy** — grabbing a pulsing power orb starts a short frenzy: all
hunters turn blue, slow down, and flee; you kill them by running through them for
bonus points.

**Special weapon crates → timed elite wave** — corner crates grant a special weapon
and spawn a wave of tougher, faster elite hunters worth far more points, backed by
an upbeat synth soundtrack, with a live countdown banner.

**Audio** — fully synthesized via the Web Audio API (no audio files): gunshots, hit
blips, kill tones, footsteps, a hurt sound, an ambient dread drone, and a proximity
heartbeat that speeds up as the nearest hunter closes in.

**HUD & minimap** — health bar, score, hunters-left, weapon and ammo, crosshair, hit
marker, damage flash, plus a top-down maze minimap (player arrow, hunter dots with
spotted-rings, pickups, power orbs, weapon crates).

## Tech

- **Rendering:** [Three.js](https://threejs.org/) `0.160.0` (ES module build via
  importmap + `examples/jsm` addons like `PointerLockControls`).
- **Audio:** Web Audio API, fully synthesized at runtime.
- **No build tooling** — everything (HTML, CSS, JS) lives in one file.

## License & attribution

Released for **demonstration and educational use**. Not for commercial use. No
warranty. This project is fan/experimental work, is **not affiliated with,
sponsored by, or endorsed by** any game publisher, and includes none of their
proprietary assets or trademarks.
