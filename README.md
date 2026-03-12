# CS2 Demo Reviewer

A browser-based CS2 demo replay viewer. Upload `.dem` or `.dem.zst` demo files and watch rounds play out on the radar with full playback controls.

All parsing runs **client-side** using WebAssembly — no server needed.

**[Live Demo](https://albedz.github.io/cs2_demo_review/)**

## Features

- Drag-and-drop `.dem` / `.dem.zst` demo upload
- 2D radar replay with player positions, health, weapons
- Smoke, molotov, HE, and flashbang visualization
- Kill feed with fade-out animations and kill lines on radar
- Collapsible scoreboard and round details panels
- Playback speeds: 0.5x, 1x, 2x, 4x, 8x, 16x
- Per-round kill log and damage breakdown
- FACEIT knife round detection (auto-skips knife/side-pick rounds)
- Correct team colors through side swaps and halftime
- Dark/light theme toggle

## Keybindings

| Key | Action |
|-----|--------|
| `Space` | Play / Pause |
| `←` `→` | Scrub forward / back |
| `Shift+←` `Shift+→` | Previous / Next round |
| `+` | Cycle playback speed |
| `1`-`9` | Jump to round |
| `H` | Toggle side panels |
| `?` | Show keybindings help |

## Supported Maps

de_anubis, de_ancient, de_overpass, de_dust2, de_inferno, de_mirage, de_nuke, de_vertigo, de_train

## Attribution

This project uses the following open-source projects:

### [demoparser2](https://github.com/LaihoE/demoparser)
- **Author:** LaihoE
- **License:** MIT
- High-performance CS2 demo parser written in Rust with WASM bindings
- Used for client-side demo parsing in the browser

### [fzstd](https://github.com/101arrowz/fzstd)
- **Author:** 101arrowz
- **License:** MIT
- High-performance Zstandard decompression library for JavaScript
- Used for client-side `.dem.zst` decompression in the browser

### [CS2 Radar Images](https://github.com/2mlml/cs2-radar-images)
- **Author:** 2mlml
- Radar overview images extracted from CS2 game files
- Used for the 2D map backgrounds in the replay viewer
