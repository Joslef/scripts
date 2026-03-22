# 🖥️ changemachine

Switches Hyprland between machine profiles by toggling tagged config lines in `hyprland.conf`.

## ✨ Features

- Two-Profile Toggle — switches between `lggram` (LG Gram laptop) and `gcube` (desktop) in one command
- Tag-Based — reads `# lggram` / `# gcube` end-of-line tags to know which lines belong to which profile
- Auto-Detection — detects the current active profile and always switches to the other
- Instant Feedback — prints which profile is now active; press Return to return to the prompt

## 🚀 Usage

```bash
changemachine
```

## ⚙️ How It Works

Lines in `~/.config/hypr/hyprland.conf` are annotated with a profile tag at the end:

```
monitor=eDP-1, 2560x1600, 0x0, 1 # lggram
# monitor=HDMI-A-1, 3840x2160, 0x0, 1 # gcube
```

The script detects the active profile by finding uncommented lines tagged `# lggram`. It then comments out all lines of the current profile and uncomments all lines of the target profile. Any line not tagged with either marker is left untouched.

## 📦 Dependencies

- Python 3 — required; must be in PATH

## 🔧 Installation

```bash
cp changemachine/changemachine ~/.local/bin/
chmod +x ~/.local/bin/changemachine
```
