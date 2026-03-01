# 🎵 audioshell

A colorful, interactive terminal radio player with an animated TUI — browse and stream 25 internet radio stations without leaving your shell.

## ✨ Features

- 📻 **25 Curated Stations** — ambient, chillout, psytrance, hip-hop, dubstep, classic 70s, and more (SomaFM, egoFM, and others)
- 🎨 **Animated Now-Playing Display** — cycling color equalizer bars and music notes animate in real time while a station is playing
- 🎛️ **Live Metadata** — shows current track title and artist, updated automatically via a Lua hook injected into mpv
- ⏸ **Pause / Resume** — suspends and resumes the mpv process with `SIGSTOP`/`SIGCONT` (no rebuffering on resume)
- 🔀 **Scrolling Station List** — list scrolls to keep the selected item centered; works at any terminal height
- 💡 **Disco Toggle** — disable the animation to reduce redraws on slow or remote terminals
- 🍎 **macOS Compatible** — detects bash 3.2 (macOS default) and adjusts `read` timeouts to integer values accordingly

## 🚀 Usage

```bash
# Launch the TUI
audioshell
```

## ⌨️ Keybindings

| Key | Action |
|-----|--------|
| `j` / `↓` | Move selection down |
| `k` / `↑` | Move selection up |
| `Space` | Play selected station |
| `p` | Pause / resume playback |
| `d` | Toggle disco animation on/off |
| `q` | Quit |

## 📻 Stations

| # | Station | Genre / Description |
|---|---------|---------------------|
| 1 | `amambient` | Ambient (stereoscenic) |
| 2 | `ambientradio` | Ambient (mrg.fm) |
| 3 | `anotherplanet` | Electronic / experimental |
| 4 | `cliqhop` | IDM / clicks & cuts (SomaFM) |
| 5 | `costadelmar` | Chillout / balearic |
| 6 | `deepspaceone` | Deep ambient (SomaFM) |
| 7 | `defcon` | Electronic / game/hacker music (SomaFM) |
| 8 | `dronezone` | Drone ambient (SomaFM) |
| 9 | `dubstep` | Dubstep (SomaFM) |
| 10 | `egochillout` | Chillout (egoFM) |
| 11 | `egoflash` | Chart / pop (egoFM) |
| 12 | `egofm` | Mainstream / pop (egoFM) |
| 13 | `egorap` | Hip-hop / rap (egoFM) |
| 14 | `egosun` | Sunshine / upbeat (egoFM) |
| 15 | `groovesalad` | Ambient / downtempo (SomaFM) |
| 16 | `groovesaladclassic` | Groove Salad classic era (SomaFM) |
| 17 | `missioncontrol` | Space-themed ambient (SomaFM) |
| 18 | `psyradio` | Psytrance |
| 19 | `schizoid` | Schizoid chill |
| 20 | `secretagent` | Lounge / spy jazz (SomaFM) |
| 21 | `seventies` | Classic 70s (SomaFM) |
| 22 | `sleepingpill` | Ultra-quiet ambient (stereoscenic) |
| 23 | `spacestation` | Space ambient (SomaFM) |
| 24 | `synphaer` | Synth / space (SomaFM) |
| 25 | `zerobeat` | Electronic (mrg.fm) |

## ⚙️ How It Works

When you press `Space` to play a station, audioshell:

1. Kills any currently running mpv process.
2. Writes a temporary Lua script to `/tmp/` that observes the `media-title` and `artist` mpv properties and writes them to a metadata file whenever they change.
3. Launches mpv in the background with `--no-video --really-quiet`, pointing at that Lua script via `--script=`.
4. On each event loop iteration, reads the metadata file and parses the track info — splitting on ` - ` if the stream embeds artist and title in a single field.

Pause/resume uses `SIGSTOP`/`SIGCONT` on the mpv PID rather than mpv's own IPC, so it works without an `--input-ipc-server` and never reconnects to the stream on resume.

The animation runs at ~3 fps using `$EPOCHREALTIME` (bash 5+). On bash 3.2 (macOS), it falls back to `$SECONDS` (1 fps) because `read -t` only accepts integer values there.

> **Note on `$EPOCHREALTIME` and locales:** `$EPOCHREALTIME` uses the system locale decimal separator. The script normalises this by replacing `,` with `.` before arithmetic, so it works correctly under locales that use a comma (e.g. `LC_NUMERIC=de_DE`).

Both the metadata file and the Lua script are cleaned up on exit via a `trap` on `EXIT` and `INT`.

## 📦 Dependencies

- `mpv` — required for all playback; must be in `PATH`

## 🔧 Installation

```bash
# Copy to a directory in your PATH
cp audioshell ~/.local/bin/
chmod +x ~/.local/bin/audioshell
```

## 🖥️ Requirements

- `bash` 3.2+ (macOS default) or `bash` 5+ (Linux, for smooth 3 fps animation)
- `mpv`
- A terminal with 256-color support
