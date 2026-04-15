# 🔐 createloginscreen

An interactive TUI for managing SDDM login themes and Quickshell lockscreen themes from the [qylock](https://github.com/Darkkal44/qylock) collection — all from a single command.

## ✨ Features

- 🖥️ **Bootscreen** — browse and apply any qylock SDDM theme with live cursor navigation
- 🔒 **Lockscreen** — set the default Quickshell lockscreen theme (read by `lock.sh` automatically)
- 📦 **Install** — installs system dependencies and runs the qylock setup scripts in one go
- 🎮 **j/k navigation** — cursor navigation through all themes, same style as `archmaint`
- 📜 **Scrollable theme list** — viewport with scroll indicators for all 25+ themes
- 🎨 **Sub-variant support** — extra options for Terraria (time/random/5 static scenes), Genshin Impact (time/random/4 backgrounds), and Clockwork (dark/light, windup toggle)
- ⚠️ **Font warnings** — alerts when a theme needs a font file that can't be bundled

## 🚀 Usage

```bash
createloginscreen
```

Navigate with `j`/`k`, confirm with `Enter`, jump directly with the shortcut key. Inside the theme picker, press `q` to cancel back to the main menu.

## 📋 Menu Options

| Key | Action |
|-----|--------|
| `b` | Set bootscreen theme (SDDM login screen) |
| `l` | Set lockscreen theme (Quickshell session lock) |
| `i` | Install qylock from repo (packages + setup scripts) |
| `0` | Exit |

## 🎨 Available Themes

Themes are read dynamically from `~/qylock/themes/`. Current collection:

| Directory | Theme |
|-----------|-------|
| `clockwork` | Clockwork |
| `dog-samurai` | Dog Samurai |
| `enfield` | Enfield |
| `forest` | Forest |
| `Genshin` | Genshin Impact ⚙️ |
| `last-of-us` | The Last of Us |
| `minecraft` | Minecraft |
| `nier-automata` | NieR: Automata |
| `ninja_gaiden` | Ninja Gaiden |
| `pixel-coffee` | Pixel · Coffee |
| `pixel-dusk-city` | Pixel · Dusk City |
| `pixel-emerald` | Pixel · Emerald |
| `pixel-hollowknight` | Pixel · Hollow Knight |
| `pixel-munchlax` | Pixel · Munchlax |
| `pixel-night-city` | Pixel · Night City |
| `pixel-rainyroom` | Pixel · Rainy Room |
| `pixel-skyscrapers` | Pixel · Skyscrapers |
| `R1999_1` | Reverse: 1999 - I |
| `R1999_2` | Reverse: 1999 - II |
| `star-rail` | Honkai: Star Rail |
| `sword` | Sword |
| `terraria` | Terraria ⚙️ |
| `windows_7` | Windows 7 |
| `winter` | Winter |
| `wuwa` | Wuthering Waves |

⚙️ = extra sub-options available after selection (also applies to `clockwork`)

## 🔤 Themes Requiring Manual Font Download

Some themes need a font file placed in `~/qylock/themes/<theme>/font/` before use:

| Theme | Font | Filename |
|-------|------|----------|
| `nier-automata` | FOT-Rodin Pro DB | `FOT-Rodin Pro DB.otf` |
| `terraria` | Andy Bold | `Andy Bold.ttf` |
| `Genshin` | HYWenHei-85W | `zhcn.ttf` |
| `sword` | The Last Shuriken | `The Last Shuriken.ttf` |
| `minecraft` | Minecraft Regular | `minecraft.ttf` |
| `star-rail` | DIN Next | `font.ttf` |

## 📦 Dependencies

**Bootscreen (SDDM):**
- `sddm`
- `qt6-declarative` `qt6-5compat` `qt6-svg`
- `qt6-multimedia` `qt6-multimedia-ffmpeg`
- `gst-plugins-base` `gst-plugins-good` `gst-plugins-bad` `gst-plugins-ugly`

**Lockscreen (Quickshell):**
- `quickshell` (AUR)
- Same Qt6/GStreamer deps as above

The **Install** menu option installs all of the above via `pacman` automatically.

## 🔧 Installation

```bash
cp createloginscreen ~/.local/bin/
chmod +x ~/.local/bin/createloginscreen
```

Requires the qylock repo to be cloned at `~/qylock` (or set `QYLOCK_DIR` env var):

```bash
git clone https://github.com/Darkkal44/qylock ~/qylock
```

## ⚙️ Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `QYLOCK_DIR` | `~/qylock` | Path to the cloned qylock repo |

Lockscreen theme is stored at `~/.config/qylock/theme` and read automatically by `lock.sh`.

## 🖥️ Requirements

- Arch Linux (or Arch-based distro)
- `bash` 4+
- `sudo` access (for SDDM install and bootscreen setup)
- Wayland compositor with `ext-session-lock-v1` support (for lockscreen — not KDE Plasma)
