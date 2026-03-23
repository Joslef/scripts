# 🔐 createloginscreen

A colorful setup script that configures the SDDM login screen with the Catppuccin Mocha Pink theme, autologin, and custom display settings — all from a single command.

## ✨ Features

- 🎨 **Theme Installation** — installs `catppuccin-sddm-theme-mocha` from the AUR via paru
- ✅ **Theme Verification** — confirms the theme directory exists before writing any config
- 📝 **SDDM Config** — writes `/etc/sddm.conf` with autologin session set to Hyprland
- 🗂️ **Drop-in Configs** — writes `theme.conf` and `autologin.conf` into `/etc/sddm.conf.d/`
- 🖋️ **Font & Clock** — configures Noto Sans (size 25) and enables the clock in the theme
- 🖼️ **Custom Background** — sets a custom background image, no user avatar shown
- ⚙️ **Service Enable** — enables the SDDM systemd service so it starts on next boot

## 🚀 Usage

```bash
# Must be run as root
sudo createloginscreen
```

## 📦 Dependencies

- [`paru`](https://github.com/Morganamilo/paru) — AUR helper used to install the theme package
- [`catppuccin-sddm-theme-mocha`](https://aur.archlinux.org/packages/catppuccin-sddm-theme-mocha) — installed automatically
- `systemctl` — to enable the SDDM service

## 🔧 Installation

```bash
cp createloginscreen ~/.local/bin/
chmod +x ~/.local/bin/createloginscreen
```

## 🖥️ Requirements

- Arch Linux (or an Arch-based distro)
- bash 4+
- Root access (`sudo`)
- SDDM installed
- Hyprland session available
