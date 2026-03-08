# MiSTeR Sync

**SNES save file synchronizer between MiSTeR FPGA and SD2SNES/FXPak Pro.**

Keep your SNES save files (.sav/.srm) in sync across both devices — always play from your latest save, no matter which hardware you used last.

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows-0078D6?logo=windows)
![License](https://img.shields.io/badge/License-MIT-green)

---

## What it does

If you own both a **MiSTeR FPGA** and an **SD2SNES/FXPak Pro**, you've probably run into the same problem: you play a game on one device, make progress, then switch to the other and find an older save — or worse, accidentally overwrite your latest one.

MiSTeR Sync solves this by comparing save files across both SD cards side by side, showing you exactly which files are synced, which have different dates, and which exist on only one device. Then it copies the newest version to the other device with a single click.

## Features

- **Side-by-side comparison** — View save files from both devices with modification dates
- **Color-coded status** — Green (synced), yellow (different dates), red (exists on one side only)
- **Smart sync** — Automatically detects the newer file and copies it to the other device, handling `.sav` ↔ `.srm` extension conversion
- **Unique file detection** — Finds saves that only exist on one device and offers to copy them across
- **MD5 integrity verification** — Validates every copy operation to ensure no data corruption
- **Optional backups** — Toggle to create timestamped `.bak` files before overwriting
- **Session logging** — Every sync operation is logged to `sync_logs/log_YYYYMMDD_HHMM.txt`
- **Configurable paths** — Edit `mister_sync.ini` to change folder paths or adapt to other systems (GBA, Genesis, etc.)
- **Sortable columns** — Click column headers to sort by filename or date
- **Drive auto-detection** — Scans all connected drives showing volume names for easy identification

## Screenshot

<!-- Add a screenshot of the app here -->
<!-- ![MiSTeR Sync](screenshot.png) -->

## Requirements

- Windows 10/11
- Python 3.8+
- `pywin32` (`pip install pywin32`)

## Installation

```bash
git clone https://github.com/YOUR_USERNAME/mister-sync.git
cd mister-sync
pip install pywin32
python MiSTeR_Sync.py
```

## Usage

1. Connect both SD cards to your PC (via USB reader or directly)
2. Run the app
3. Select the MiSTeR FPGA drive and the SD2SNES drive from the dropdown menus
4. Click **Cargar** to load and compare save files
5. Review the color-coded status of each file
6. Optionally enable **"Crear backup antes de sobrescribir"** for extra safety
7. Click **Sincronizar** to sync — you'll be prompted to confirm each operation

## Default folder structure

The app expects this default layout (configurable via `mister_sync.ini`):

```
MiSTeR SD card:          SD2SNES SD card:
├── saves/               ├── sd2snes/
│   └── SNES/            │   └── saves/
│       ├── game.sav     │       ├── game.srm
│       └── ...          │       └── ...
```

## Configuration

On first run, a `mister_sync.ini` file is created with defaults:

```ini
[PATHS]
ruta_a = saves\SNES
ruta_b = sd2snes\saves
extension_a = .sav
extension_b = .srm
log_dir = sync_logs
```

Edit these values to adapt to different consoles or custom folder structures.

## How sync works

1. Files are matched by **name** (ignoring extension), so `Zelda.sav` on MiSTeR matches `Zelda.srm` on SD2SNES
2. If both exist and have **different dates**, the newer one is copied over the older one (with extension conversion)
3. If a file exists on **only one device**, it's offered for copy to the other
4. A 2-second tolerance is used for timestamp comparison to handle FAT32 filesystem quirks
5. Every operation is logged with timestamps

## License

MIT
