# 🛠️ archmaint

A colorful, interactive Arch Linux maintenance script that keeps your system clean and healthy — all from a single command.

## ✨ Features

- 📦 **Full System Update** — runs `pacman -Syu` with confirmation prompt
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

# Non-interactive quick maintenance (update + orphans + cache + db check + info)
archmaint --quick
```

## 📋 Menu Options

| Option | Action |
|--------|--------|
| `1` | Full system update |
| `2` | Remove orphan packages |
| `3` | Clean package cache |
| `4` | Check package database |
| `5` | List foreign/AUR packages |
| `6` | System info |
| `7` | ⚡ Quick mode (all safe ops, no prompts) |
| `8` | Run all tasks interactively |
| `0` | Exit |

## 📦 Dependencies

- `pacman` (standard on Arch)
- `paccache` from `pacman-contrib` (optional, for cache cleanup — falls back to `pacman -Sc` if missing)

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
