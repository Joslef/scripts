# 📦 pkgsync

A colorful, interactive tool that automatically syncs your Arch Linux package lists to a GitHub repository — on a schedule, on boot, or on demand.

## ✨ Features

- 🕐 **Scheduled Syncing** — set an hourly, daily, or weekly systemd timer with a single menu selection
- 🚀 **Boot Sync** — optional service that syncs 30 seconds after boot, once the network is up
- 📋 **Dual Package Lists** — exports native packages (`pkglist-native.txt` via `pacman -Qqen`) and AUR/foreign packages (`pkglist-aur.txt` via `pacman -Qqem`) separately
- 🔄 **Change Detection** — skips the commit and push entirely if the package lists have not changed since the last sync
- 🐙 **GitHub Integration** — pushes to your GitHub repo via `git`; validates access with `gh` before saving any URL
- 🛠️ **Interactive Configuration** — change the save path or GitHub repo at any time without touching config files manually
- 📊 **Live Status** — shows timer schedule, next scheduled run, boot sync state, save path, and target repo at a glance
- ⚡ **Headless Mode** — pass `--run` for silent, non-interactive execution (used internally by systemd)

## 🚀 Usage

```bash
# Open the interactive menu
pkgsync

# Run a sync directly (non-interactive — used by systemd units)
pkgsync --run
```

On first launch, pkgsync will prompt for two required values:

1. **Save path** — an absolute local directory where the git repo (and package list files) will live. Created automatically if it does not exist.
2. **GitHub repo URL** — the `https://github.com/...` URL of the repository to push to. A `.git` suffix is appended automatically if omitted.

Both values are persisted to `~/.config/pkgsync/config` and reused on subsequent runs.

## 📋 Menu Options

| Option | Action |
|--------|--------|
| `1` | Set schedule: Hourly |
| `2` | Set schedule: Daily (prompts for time) |
| `3` | Set schedule: Weekly (prompts for day and time) |
| `4` | Toggle boot sync on/off |
| `a` | Change save path |
| `b` | Change GitHub repo URL |
| `5` | Run sync now |
| `6` | Show current status |
| `7` | Disable / remove timer or boot sync |
| `0` | Exit |

## ⚙️ How It Works

Each sync (`--run`) does the following:

1. Writes `pkglist-aur.txt` and `pkglist-native.txt` into the configured save path.
2. Checks whether either file has changed (`git diff`). If nothing changed, it exits silently.
3. Stages both files, commits with a `YYYY-MM-DD_HH-MM` timestamp as the message, and pushes to `origin main`.

Scheduling is handled entirely by user-level systemd units written to `~/.config/systemd/user/`. No root access is required.

## 📦 Dependencies

- `pacman` (standard on Arch)
- `git` — for committing and pushing package lists
- `gh` (GitHub CLI) from `github-cli` — used to validate repository access before saving a URL; must be authenticated via `gh auth login`
- `systemd` — for the timer and boot service units (user session)
- `timedatectl` — used to display the local timezone in schedule descriptions

## 🔧 Installation

```bash
# Copy to a directory in your PATH
cp pkgsync ~/.local/bin/
chmod +x ~/.local/bin/pkgsync
```

Authenticate the GitHub CLI before running pkgsync for the first time:

```bash
gh auth login
```

## 🖥️ Restoring Packages on a New Machine

To recreate your package set on a fresh Arch installation, clone your GitHub package-list repo and replay both lists.

```bash
# 1. Clone the repo containing your saved package lists
git clone https://github.com/your-username/your-pkglist-repo
cd your-pkglist-repo

# 2. Install all native (official repo) packages
sudo pacman -S --needed - < pkglist-native.txt

# 3. Install AUR packages — requires an AUR helper (e.g. yay or paru)
yay -S --needed - < pkglist-aur.txt
```

Install your AUR helper (e.g. `yay`) before running step 3; it is not available via pacman by default.

## 🖥️ Requirements

- Arch Linux (or an Arch-based distro)
- `bash` 4+
- A GitHub account with a repository to push package lists to
- `gh` CLI authenticated (`gh auth login`)
