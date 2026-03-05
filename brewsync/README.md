# 🍺 brewsync

A colorful, interactive tool that automatically syncs your Homebrew and Mac App Store package lists to a GitHub repository — on a schedule or on demand.

## ✨ Features

- 🕐 **Scheduled Syncing** — set an hourly, daily, or weekly launchd timer with a single menu selection
- 📋 **Triple Package Lists** — exports Homebrew formulae (`brewlist-formula.txt`), casks (`brewlist-cask.txt`), and Mac App Store apps (`maslist.txt`) separately
- 🔄 **Change Detection** — skips the commit and push entirely if the package lists have not changed since the last sync
- 🐙 **GitHub Integration** — pushes to your GitHub repo via `git`; validates access with `gh` before saving any URL
- 🛠️ **Interactive Configuration** — change the save path or GitHub repo at any time without touching config files manually
- 📊 **Live Status** — shows timer schedule, LaunchAgent state, save path, target repo, and per-list item counts at a glance
- ⚡ **Headless Mode** — pass `--run` for silent, non-interactive execution (used internally by launchd)
- 📥 **Restore from Repo** — pulls the package lists from the GitHub repo and installs any packages that are present in the repo but missing locally, using the correct installer (`brew install` for formulae, `brew install --cask` for casks, `mas install` for MAS apps); additive only — locally installed packages that are absent from the repo are never removed

## 🚀 Usage

```bash
# Open the interactive menu
brewsync

# Run a sync directly (non-interactive — used by launchd)
brewsync --run
```

On first launch, brewsync will prompt for two required values:

1. **Save path** — an absolute local directory where the git repo (and package list files) will live. Created automatically if it does not exist.
2. **GitHub repo URL** — the `https://github.com/...` URL of the repository to push to. A `.git` suffix is appended automatically if omitted.

Both values are persisted to `~/.config/brewsync/config` and reused on subsequent runs.

## 📋 Menu Options

| Option | Action |
|--------|--------|
| `1` | Set schedule: Hourly |
| `2` | Set schedule: Daily (prompts for time) |
| `3` | Set schedule: Weekly (prompts for day and time) |
| `a` | Change save path |
| `b` | Change GitHub repo URL |
| `c` | Restore from repo |
| `5` | Run sync now |
| `6` | Show current status |
| `7` | Disable / remove LaunchAgent |
| `0` | Exit |

## ⚙️ How It Works

Each sync (`--run`) does the following:

1. Writes `brewlist-formula.txt`, `brewlist-cask.txt`, and `maslist.txt` into the configured save path.
2. Checks whether any file has changed (`git diff --cached`). If nothing changed, it exits silently.
3. Stages all three files, commits with a `YYYY-MM-DD_HH-MM` timestamp as the message, and pushes to `origin main`.

`maslist.txt` is populated by `mas list` if `mas` is installed. If `mas` is absent, an empty file is created on first run so git tracking stays clean.

Scheduling is handled by a user-level LaunchAgent plist written to `~/Library/LaunchAgents/`. No root access is required. Logs are written to `~/.config/brewsync/brewsync.log` and `~/.config/brewsync/brewsync.err`.

## 📦 Dependencies

- `brew` (Homebrew) — generates the formula and cask lists
- `git` — for committing and pushing package lists
- `gh` (GitHub CLI) — used to validate repository access before saving a URL; must be authenticated via `gh auth login`; install with `brew install gh`
- `mas` (Mac App Store CLI) — optional; generates `maslist.txt`; install with `brew install mas`; if absent, an empty `maslist.txt` is maintained

## 🔧 Installation

```bash
# Copy to a directory in your PATH
cp brewsync ~/.local/bin/
chmod +x ~/.local/bin/brewsync
```

Authenticate the GitHub CLI before running brewsync for the first time:

```bash
gh auth login
```

## 🖥️ Restoring Packages on a New Machine

The quickest way to restore your package set is the built-in `c) Restore from repo` menu option. It pulls the saved lists from your GitHub repo and installs any packages missing locally using the correct installer for each list. It is additive only — packages installed locally but absent from the repo are left untouched.

For a fully manual restore (or when running brewsync is not yet possible), clone the repo and replay the lists directly:

```bash
# 1. Clone the repo containing your saved package lists
git clone https://github.com/your-username/your-brewlist-repo
cd your-brewlist-repo

# 2. Install all Homebrew formulae
xargs brew install < brewlist-formula.txt

# 3. Install all Homebrew casks
xargs brew install --cask < brewlist-cask.txt

# 4. Install Mac App Store apps (requires mas)
awk '{print $1}' maslist.txt | xargs mas install
```

Homebrew must be installed before running steps 2 and 3; `mas` must be installed and you must be signed into the App Store before running step 4.

## 🖥️ Requirements

- macOS (Intel or Apple Silicon — PATH includes both `/opt/homebrew/bin` and `/usr/local/bin`)
- `bash` 4+
- A GitHub account with a repository to push package lists to
- `gh` CLI authenticated (`gh auth login`)
