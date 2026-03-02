# 🔍 gitstatus

A colorful, interactive Git repository status checker. Recursively scans a directory tree, fetches remotes, and gives you a clear overview of every repo's health at a glance.

## ✨ Features

- 🔎 **Recursive Scanning** — finds every `.git` repo under a given directory
- 🌐 **Remote Fetch** — runs `git fetch` on each repo before checking status
- 🚨 **Dirty Detection** — flags repos with any of the following issues:
  - ✗ Modified (unstaged) files
  - ✗ Untracked files
  - ✗ Unpushed commits (ahead of remote)
  - ⚠ Behind remote (pull needed)
  - ⚠ Staged but uncommitted changes
- 🎯 **Dirty-only Filter** — toggle to show only repos that need attention
- 📂 **Custom Path Scanning** — enter any path directly from the menu
- ⚡ **Non-interactive Mode** — pass `--scan` to pipe results to other tools
- 🌀 **Animated Spinner** — braille spinner keeps you informed during long scans
- 📊 **Summary Stats** — total / clean / needs-attention counts at the end

## 🚀 Usage

```bash
# Interactive menu (scans current directory)
gitstatus

# Interactive menu (scans a specific directory)
gitstatus ~/projects

# Non-interactive scan and exit (all repos)
gitstatus --scan ~/projects
gitstatus -s ~/projects

# Non-interactive scan, dirty repos only
gitstatus --scan --dirty ~/projects
gitstatus -s -d ~/projects
```

## 📋 Menu Options

| Option | Action |
|--------|--------|
| `1` | Scan all repos in current path |
| `2` | Scan repos in a custom path |
| `3` | Toggle dirty-repos-only filter |
| `0` | Exit |

### Non-interactive flags

| Flag | Description |
|------|-------------|
| `--scan` / `-s` | Run a scan and exit (no menu) |
| `--dirty` / `-d` | (after `--scan`) Show dirty repos only |

## 🎨 Output Key

| Symbol | Meaning |
|--------|---------|
| ✓ (green) | Repository is clean |
| ▶ (pink) | Repository needs attention |
| ✗ (red) | Modified files / untracked files / unpushed commits |
| ⚠ (yellow) | Behind remote / staged changes |

## 🔧 Installation

```bash
# Copy to a directory in your PATH
cp gitstatus ~/.local/bin/
chmod +x ~/.local/bin/gitstatus
```

## 🖥️ Requirements

- `bash` 4+
- `git`
- A terminal with 256-color support (for the pink color scheme)
