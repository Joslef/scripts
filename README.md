# 🧰 scripts

A collection of colorful, interactive shell scripts for system maintenance, media, and automation.

## 📜 Scripts

| Script | Description | Platform | Highlights |
|--------|-------------|----------|------------|
| [archmaint](archmaint/) | Interactive Arch Linux maintenance — system updates, orphan removal, cache cleanup, database checks | Linux | Quick mode (`--quick`), run-all option, system info dashboard |
| [audioshell](audioshell/) | Terminal radio player with animated TUI — browse and stream 25 internet radio stations | Both | Live metadata, animated equalizer, pause/resume, disco toggle, 25 curated stations |
| [brewsync](brewsync/) | Syncs Homebrew and Mac App Store package lists to GitHub — scheduled or on demand | macOS | Launchd timers (hourly/daily/weekly), restore from repo, change detection |
| [chezclaudesync](chezclaudesync/) | Syncs Claude Code config files into chezmoi for version-controlled backup | Both | Settings, agents, hooks, memory files; secrets-safe (no API keys) |
| [gitstatus](gitstatus/) | Recursive Git repo health checker — scans directories and flags dirty repos | Both | Remote fetch, dirty-only filter, non-interactive mode (`--scan`), animated spinner |
| [macfresh](macfresh/) | Interactive macOS maintenance — Homebrew updates, App Store updates, system cleanup | macOS | Quick mode (`--run`), formula/cask/MAS updates, cache cleanup, brew doctor |
| [pkgsync](pkgsync/) | Syncs Arch Linux package lists to GitHub — scheduled, on boot, or on demand | Linux | Systemd timers, boot sync, restore from repo, AUR helper detection |

---

### 🛠️ archmaint

Interactive Arch Linux maintenance — system updates, orphan removal, cache cleanup, and database checks. Supports a quick non-interactive mode.

→ [Full documentation](archmaint/README.md) | `archmaint` or `archmaint --quick`

---

### 🎵 audioshell

A terminal radio player with an animated TUI — browse and stream 25 curated internet radio stations without leaving your shell. Supports pause/resume with no rebuffering.

→ [Full documentation](audioshell/README.md) | `audioshell`

---

### 🍺 brewsync

Syncs Homebrew formulae, casks, and Mac App Store package lists to a GitHub repository on a launchd schedule or on demand. Also restores packages from the repo on a new machine.

→ [Full documentation](brewsync/README.md) | `brewsync` or `brewsync --run`

---

### 🤖 chezclaudesync

Syncs Claude Code config files — settings, agents, hooks, and memory files — into chezmoi for version-controlled backup. Secrets-safe: API keys are never included.

→ [Full documentation](chezclaudesync/README.md) | `chezclaudesync`

---

### 📊 gitstatus

Recursively scans a directory tree and reports the health of every Git repository found — uncommitted changes, untracked files, unpushed commits, and more.

→ [Full documentation](gitstatus/README.md) | `gitstatus` or `gitstatus --scan`

---

### 🍏 macfresh

Interactive macOS maintenance — Homebrew formula and cask updates, Mac App Store updates, system cache cleanup, and brew doctor checks. Supports a quick non-interactive mode.

→ [Full documentation](macfresh/README.md) | `macfresh` or `macfresh --run`

---

### 📦 pkgsync

Syncs Arch Linux package lists to a GitHub repository via systemd timers, on boot, or on demand. Detects AUR helpers automatically and restores packages on a new machine.

→ [Full documentation](pkgsync/README.md) | `pkgsync` or `pkgsync --run`

---

## 🔧 Installation

Each script is self-contained. Copy any script to a directory in your `PATH`:

```bash
# Copy any script to a directory in your PATH
cp <script-dir>/<script> ~/.local/bin/
chmod +x ~/.local/bin/<script>
```

See each script's README for dependency requirements and first-run configuration.

## 🔗 Related Repos

- [Joslef/dotfiles](https://github.com/Joslef/dotfiles) — chezmoi-managed dotfiles
- [Joslef/macOS_homebrewlist](https://github.com/Joslef/macOS_homebrewlist) — Homebrew package backup (managed by brewsync)
- [Joslef/CachyOS_pkglist](https://github.com/Joslef/CachyOS_pkglist) — Arch package backup (managed by pkgsync)
