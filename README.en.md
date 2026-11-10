# LASERTAG Configurator for macOS

[Русский](README.md) | **English**

Unofficial configurator for LaserWar devices on Mac — Apple Silicon (M1–M4) and Intel.

- **Devices** are configured via the Smart Remote PRO (USB): Smart control point 2.0, Smart medkit 2.0,
  Smart medic, Command post, and devices marked “(test)” — universal point, bomb, “Dome” system,
  universal remote, artefact, hostage, zombie, vest / helmet, grenade launcher.
- **Game statistics (test)** — reading generation 7, 8 and 9 taggers over Bluetooth, rating, ranks, teams,
  game files `.xml` (compatible with the Windows configurator) and a PDF report.
- Settings presets, exchange log for diagnostics, Russian and English interface.

## Requirements

| | |
|---|---|
| macOS | **12 Monterey or newer** (13 Ventura, 14 Sonoma, 15 Sequoia, 26 Tahoe) |
| Processor | Apple Silicon (M1, M2, M3, M4) or Intel |
| Devices | Smart Remote PRO and a USB cable; no driver needed |
| Statistics | Bluetooth on the Mac and paired generation 7–9 taggers |

You don't need to install .NET or anything else — everything is bundled inside the app.

## Download

Open the **[Releases](../../releases/latest)** page and download the archive for your Mac:

| Your Mac | File |
|---|---|
| Apple Silicon (M1/M2/M3/M4) | `LaserTag-mac-arm64.tar.gz` |
| Intel | `LaserTag-mac-x64.tar.gz` |

Not sure which processor you have? Apple menu → **About This Mac**: a “Chip” line (Apple M…) means Apple Silicon,
a “Processor” line (Intel …) means Intel.

## Installation

### Option 1. Manually

1. Double-click the downloaded archive — `LaserTag.app` appears next to it.
2. Drag `LaserTag.app` into the **Applications** folder.
3. The app is not signed with an Apple certificate, so macOS blocks it on first launch.
   Open **Terminal** (Applications → Utilities) and run:

   ```bash
   xattr -cr /Applications/LaserTag.app
   ```

4. Launch LaserTag from Applications or Launchpad.

If macOS still says the app “is damaged” or “cannot be opened”:

```bash
codesign --force --deep -s - /Applications/LaserTag.app
```

Without Terminal: right-click the app → **Open** → **Open**.
On macOS 15 Sequoia and newer: try to open the app, then go to
**System Settings → Privacy & Security** and click **Open Anyway**.

### Option 2. With the script

Also download `install-mac.sh` from the Releases page and put it next to the archive (usually in Downloads).
In Terminal:

```bash
cd ~/Downloads
bash install-mac.sh
```

The script picks the archive for your processor, installs the app into Applications, removes the quarantine and launches it.
If Safari has already unpacked the archive (Downloads contains `LaserTag.app` instead of `.tar.gz`), use option 1.

### Error −36 (“The operation can’t be completed”)

This happens when the archive is on a network share or in a virtual machine's shared folder.
Copy the archive to the Mac's disk first (e.g. to Downloads), then unpack and install from there.

### Updating and removing

- Update: download the new archive and replace `LaserTag.app` in Applications (then run `xattr -cr …` again).
- Remove: drag `LaserTag.app` to the Trash. Settings are stored in `~/Library/Application Support/LaserTag`,
  presets and statistics in `~/Documents/LASERTAG`.

The interface language is switched in the app (Russian / English).

## Getting started

### Configuring devices via the remote

1. Connect the Smart Remote PRO with a USB cable and switch it on.
2. Click **Connect remote** at the bottom of the window — the port and protocol are detected automatically.
3. Select a device on the left and point the remote at its IR receiver (1–2 m).
4. **Check link** → **Read** (if the device supports it) → change the fields → **Write**.

### Statistics over Bluetooth

1. Switch the tagger on. **System Settings → Bluetooth** → select `LW_RIFLE`, `LW_RIFLE_V8`
   or `BIATHLON_V8` → PIN code **1234**.
2. In the app: **Game → Statistics**, click **Refresh**. On first use macOS asks for Bluetooth
   access — click **Allow** (or enable LaserTag in **Privacy & Security → Bluetooth**).
3. Tick the taggers and click **Read selected**. Taggers with identical names are distinguished by the end
   of their address; after the first read the player ID is shown next to them.
4. **PDF report…** creates a printable report.

## Limitations

- Devices and sections marked **“(test)”** have been ported from the Windows version but not yet checked on all
  hardware. After writing, check the result on the device; compare statistics with the Windows configurator.
- The program is unofficial and not signed by Apple.

## Feedback

Found a bug? Open an [Issue](../../issues) and attach the exchange log text from the app window
(it shows at which step the problem occurred), your macOS version and Mac model.
