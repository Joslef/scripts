# 📸 photoimport

A colorful photo import script that organises photos from a flat import folder into a `yyyy/mm/dd` directory hierarchy based on EXIF creation date.

## ✨ Features

- 📅 **EXIF-aware dating** — reads `DateTimeOriginal` first, falls back to `CreateDate`, then `FileModifyDate`
- 🔢 **Zero-date skipping** — ignores corrupt `0000:00:00` timestamps automatically
- 🗂️ **Auto folder creation** — creates `yyyy/mm/dd` subfolders under the destination as needed
- 🔁 **Idempotent** — skips files that already exist at the destination
- 🌍 **All formats** — handles JPG, HEIC, MOV, MP4, PNG, and anything exiftool can read
- ⚡ **Fast bulk EXIF read** — single `exiftool -csv` call for the entire import folder
- 🔍 **Dry-run mode** — preview what would be copied without touching any files
- 📊 **Clear summary** — reports copied, skipped, and undatable files at the end

## 🚀 Usage

```bash
# Import from default source into default destination
photoimport

# Preview only — no files written
photoimport --dry-run

# Skip confirmation prompt
photoimport --run

# Custom source and destination
photoimport /path/to/import /path/to/library

# Combine flags
photoimport --dry-run /path/to/import /path/to/library
```

## 📋 Arguments & Flags

| Argument / Flag | Description | Default |
|-----------------|-------------|---------|
| `SOURCE` | Flat folder containing photos to import | `/mnt/vault/Bilder/Fotos/import` |
| `DEST` | Root of the photo library (`yyyy/mm/dd` structure lives here) | `/mnt/vault/Bilder/Fotos` |
| `--dry-run` / `-n` | Preview mode — prints what would happen, writes nothing | off |
| `--run` / `-y` | Skip the confirmation prompt | off |
| `--help` / `-h` | Show help and exit | — |

## 📅 Date Priority

Files are sorted by the best available date, tried in this order:

1. **`DateTimeOriginal`** — set by the camera at capture time (most reliable)
2. **`CreateDate`** — file creation date embedded by the device
3. **`FileModifyDate`** — filesystem modification time (last resort)

Timestamps of `0000:00:00` are treated as missing and the next source is tried.
Files where no valid date can be found are reported in the summary but not copied.

## 📦 Dependencies

- `exiftool` — EXIF metadata reader (`sudo pacman -S perl-image-exiftool`)
- `python3` — standard on most Linux systems

## 🔧 Installation

```bash
cp photoimport ~/.local/bin/
chmod +x ~/.local/bin/photoimport
```

## 🖥️ Requirements

- Linux (or any system with `bash` 4+)
- `exiftool`
- `python3`
