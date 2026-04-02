# 🖥️ switchreso

Quickly switch monitor resolutions on a dual-monitor Hyprland setup from a simple TUI menu.

## ✨ Features

- 🗂️ **Two-level TUI menu** — select a resolution preset, then choose which display to apply it to
- 📐 **Resolution presets** — supports 4K, 2K, 1080p, and Steamdeck layouts
- 🖥️ **Per-display or dual switching** — apply changes to left, right, or both monitors simultaneously
- 🔄 **Reset to default** — restore both displays to 4K with a single selection
- 📏 **Automatic position recalculation** — adjusts right monitor offset when left monitor width changes

## 🚀 Usage

```bash
switchreso
```

## 📋 Menu Options

### Resolution Presets

| Option | Action |
|---|---|
| `4K` | Switch to 3840×2160@60Hz |
| `2K` | Switch to 2560×1440@60Hz |
| `1080p` | Switch to 1920×1080@60Hz |
| `Steamdeck` | Switch to 1280×800@60Hz |
| `Reset` | Restore both displays to 4K default |

### Display Selection

| Option | Action |
|---|---|
| `Display Left` | Apply to HDMI-A-1 |
| `Display Right` | Apply to DP-1 |
| `Both` | Apply to both monitors |

## 📦 Dependencies

- `hyprctl` (Hyprland)
- `python3` (for JSON parsing)

## 🔧 Installation

```bash
cp switchreso ~/scripts/switchreso/
chmod +x ~/scripts/switchreso/switchreso
```

> Requires Hyprland with a dual monitor setup using HDMI-A-1 (Display Left) and DP-1 (Display Right).
