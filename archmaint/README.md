# 🛠️ archmaint

A colorful, interactive Arch Linux maintenance script that keeps your system clean and healthy — all from a single command.

## ✨ Features

- 📦 **Full System Update** — runs `pacman -Syu` with confirmation prompt
- 🔁 **AUR Update** — updates AUR packages via `paru`
- 📱 **AppImage Update** — updates AppImages via `appimageupdatetool`, sourcing paths from [pkgsync](../pkgsync/)'s `pkglist-appimage.txt` (falls back to scanning `~/` at depth 4)
- 🧹 **Orphan Removal** — detects and removes packages no longer needed as dependencies
- 💾 **Cache Cleanup** — flexible paccache integration with 4 cleanup strategies (keep 3, keep 1, remove uninstalled, dry run)
- 🔍 **Database Check** — validates the pacman database for errors
- 🌍 **Foreign/AUR Package Listing** — shows all packages not from official repos
- 📊 **System Info** — disk usage, package counts (total, explicit, orphans, foreign, cached)
- ⚡ **Quick Mode** — runs all safe operations non-interactively with a single flag
- 🎮 **Run All** — steps through every maintenance task interactively in sequence

## 🚀 Usage

```bash
# Interactive menu
archmaint

# Non-interactive quick maintenance (update + AUR + AppImages + orphans + cache + db check + info)
archmaint --quick
```

## 📋 Menu Options

| Key | Action |
|-----|--------|
| `q` | ⚡ Quick mode (all safe ops, no prompts) |
| `u` | Full system update |
| `a` | AUR update (paru) |
| `p` | AppImage update (appimageupdatetool) |
| `o` | Remove orphan packages |
| `c` | Clean package cache |
| `d` | Check package database |
| `f` | List foreign/AUR packages |
| `i` | System info |
| `r` | Run all tasks interactively |
| `0` | Exit |

Navigate with `j`/`k`, select with Enter, or jump directly with the key.

## 📦 Dependencies

- `pacman` (standard on Arch)
- `paru` (optional, for AUR updates)
- `paccache` from `pacman-contrib` (optional, for cache cleanup — falls back to `pacman -Sc` if missing)
- `appimageupdatetool` from AUR (optional, for AppImage updates — `paru -S appimageupdatetool-bin`)

## 🔗 pkgsync Integration

When [pkgsync](../pkgsync/) is configured, `archmaint` reads the AppImage path list from its `pkglist-appimage.txt` instead of scanning the filesystem. This makes AppImage updates instant — no directory traversal needed.

## 🔧 Installation

```bash
# Copy to a directory in your PATH
cp archmaint ~/.local/bin/
chmod +x ~/.local/bin/archmaint
```

## 🖥️ Requirements

- Arch Linux (or an Arch-based distro)
- `bash` 4+
- `sudo` access
