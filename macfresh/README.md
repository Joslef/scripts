# 🍎 macfresh

A colorful, interactive macOS maintenance script that keeps your Homebrew environment and system clean and healthy — all from a single command.

## ✨ Features

- 📦 **Formulae Update** — runs `brew update` + `brew upgrade --formula` with confirmation prompt
- 🖥️ **Casks Update** — upgrades GUI apps via `brew upgrade --cask` (warns that casks may require passwords)
- 🛍️ **Mac App Store Update** — lists outdated apps and upgrades via `mas`
- 🛡️ **Safe Update** — updates formulae and App Store apps while skipping casks (lower risk)
- 🔄 **Full Update** — updates formulae, casks, and App Store apps in sequence
- 🧹 **Homebrew Cleanup** — flexible cleanup with 4 strategies: standard, aggressive (prune all + cache), dry run, or skip
- 🩺 **Homebrew Doctor** — checks Homebrew for configuration issues and reports results
- 🗑️ **System Cleanup** — clears `~/Library/Caches` and/or `~/Library/Logs` with size preview before deletion
- 📊 **System Info** — macOS version, disk usage, formulae/cask/App Store app counts, and Homebrew cache size
- ⚡ **Quick Mode** — non-interactively runs safe update, cleanup, doctor check, and system info with a single flag
- 🎮 **Run All** — steps through every maintenance task interactively in sequence

## 🚀 Usage

```bash
# Interactive menu
macfresh

# Non-interactive quick maintenance (safe update + cleanup + doctor + info)
macfresh --quick
```

## 📋 Menu Options

| Option | Action |
|--------|--------|
| `1` | Homebrew formulae update |
| `2` | Homebrew casks update |
| `3` | Mac App Store update |
| `4` | Safe update (formulae + App Store, no casks) |
| `5` | Full update (formulae + casks + App Store) |
| `6` | Homebrew cleanup |
| `7` | Homebrew doctor |
| `8` | System cleanup (caches and logs) |
| `9` | System info |
| `q` | ⚡ Quick mode (safe ops, no prompts) |
| `a` | Run all tasks interactively |
| `0` | Exit |

## 📦 Dependencies

- `brew` — Homebrew, required; install from https://brew.sh
- `mas` — Mac App Store CLI (optional, install: `brew install mas`; App Store updates unavailable without it)

## 🔧 Installation

```bash
cp macfresh ~/.local/bin/
chmod +x ~/.local/bin/macfresh
```

## 🖥️ Requirements

- macOS
- `bash` 4+
