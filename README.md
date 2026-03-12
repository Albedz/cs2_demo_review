# CS2 Demo Reviewer

A browser-based CS2 demo replay viewer. Upload `.dem` or `.dem.zst` demo files and watch rounds play out on the radar with full playback controls.

All parsing runs **client-side** using WebAssembly — no server needed. Works on GitHub Pages or any static file host.

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

## Running Locally

### Option 1: Static file server (client-side only)

Any static HTTP server will work:

```bash
# Python
python3 -m http.server 8000

# Node.js
npx serve .

# Then open http://localhost:8000
```

### Option 2: Flask server (server-side parsing)

The Flask server parses demos on the backend and can list `.dem.zst` files in the project directory.

```bash
# Create virtual environment
python3 -m venv .venv
source .venv/bin/activate  # or .venv/bin/activate.fish for fish shell

# Install dependencies
pip install flask demoparser2 pandas

# Start server
./start.sh
# or: .venv/bin/python3 server.py

# Open http://localhost:5555
```

Requires `zstd` CLI tool for `.dem.zst` decompression in server mode.

## GitHub Pages

This project works on GitHub Pages out of the box. Push the repo and enable Pages from the repository settings. The entry point is `index.html` in the root directory.

**Required files for the client-side viewer:**
```
index.html              # Main viewer (client-side)
lib/demoparser2.js      # WASM JS bindings
lib/demoparser2_bg.wasm # WASM binary
lib/fzstd.js            # Zstd decompression
static/radars/*.png     # Radar images
```

## Project Structure

```
index.html          # Client-side viewer (GitHub Pages compatible)
static/index.html   # Server-side viewer (used by Flask)
server.py           # Flask backend for server-side parsing
review.py           # CLI demo review tool (terminal)
start.sh            # Server restart script
lib/                # WASM and JS libraries
static/radars/      # Radar images and coordinate data
```

## Supported Maps

de_anubis, de_ancient, de_overpass, de_dust2, de_inferno, de_mirage, de_nuke, de_vertigo, de_train

## Attribution

This project uses the following open-source projects:

### [demoparser2](https://github.com/LaihoE/demoparser)
- **Author:** LaihoE
- **License:** MIT
- High-performance CS2 demo parser written in Rust with Python and WASM bindings
- Used for parsing demo files both server-side (Python) and client-side (WASM)

### [fzstd](https://github.com/101arrowz/fzstd)
- **Author:** 101arrowz
- **License:** MIT
- High-performance Zstandard decompression library for JavaScript
- Used for client-side `.dem.zst` decompression in the browser

### [CS2 Radar Images](https://github.com/2mlml/cs2-radar-images)
- **Author:** 2mlml
- Radar overview images extracted from CS2 game files
- Used for the 2D map backgrounds in the replay viewer

### [Flask](https://flask.palletsprojects.com/)
- **License:** BSD-3-Clause
- Python web framework used for the optional server-side backend

### [Rich](https://github.com/Textualize/rich)
- **Author:** Textualize
- **License:** MIT
- Used in the CLI review tool (`review.py`) for terminal formatting

### [pandas](https://pandas.pydata.org/)
- **License:** BSD-3-Clause
- Used in the server-side parser for data manipulation
