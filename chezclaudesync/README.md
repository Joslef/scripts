# 🤖 chezclaudesync

Syncs Claude Code (`~/.claude`) configuration files into chezmoi so your settings, agents, hooks, and memory files are backed up to version control — without leaking API keys or session data.

## ✨ Features

- ⚙️ **Settings Sync** — tracks `settings.json` and `settings.local.json`
- 🪝 **Hooks and Agents** — adds every file inside `~/.claude/hooks/` and `~/.claude/agents/`
- 🧠 **Project Memory** — captures per-project `MEMORY.md` files from `~/.claude/projects/*/memory/`
- 🗂️ **Agent Memory** — captures all `.md` files under `~/.claude/agent-memory/*/`
- 🔒 **Secrets-safe** — only adds the files listed above; API keys, session tokens, and ephemeral state are never touched
- 📊 **Summary Output** — prints the count of files successfully added on every run

## 🚀 Usage

```bash
# Run manually whenever you want to snapshot your current Claude config
chezclaudesync
```

After the script runs, use the normal chezmoi workflow to review and push:

```bash
chezmoi diff          # review what changed
chezmoi cd            # open the chezmoi source directory
git add -A && git commit -m "chore: sync claude config"
git push
```

## 📂 What Gets Tracked

| Path | Description |
|------|-------------|
| `~/.claude/settings.json` | Global Claude Code settings |
| `~/.claude/settings.local.json` | Local overrides (machine-specific settings) |
| `~/.claude/statusline-command.sh` | Custom statusline command script |
| `~/.claude/agents/` | All files in the agents directory |
| `~/.claude/hooks/` | All files in the hooks directory |
| `~/.claude/projects/*/memory/MEMORY.md` | Per-project persistent memory files |
| `~/.claude/agent-memory/*/*.md` | Agent-specific memory markdown files |

## 🔒 What Is Excluded

Everything not in the table above, including:

- API keys and credentials
- Session and authentication tokens
- Project conversation history and chat logs
- Cached completions and ephemeral runtime state
- Any other files chezmoi does not already manage

The script uses an explicit allowlist — it only calls `chezmoi add` on known-safe paths, so new files created by Claude Code will not be accidentally swept into version control until you deliberately add them to the script.

## 📦 Dependencies

- `fish` — the script is written in fish shell
- `chezmoi` — must be installed and initialized (`chezmoi init` already run)

## 🔧 Installation

```bash
cp ~/scripts/chezclaudesync/chezclaudesync ~/.local/bin/
chmod +x ~/.local/bin/chezclaudesync
```

## 🖥️ Requirements

- CachyOS / Arch Linux (or any distro with fish and chezmoi available)
- `fish` shell
- `chezmoi` initialized with a remote repository
