# Mazduino Tuner

Desktop tuning software for Mazduino ECUs (rusEFI based) on Windows.

> **Alpha.** Mazduino Tuner is still being tested. Expect rough edges, keep a copy of your
> tune (`.msq` or `.mdt`) before writing to an ECU, and do not rely on it for an engine you
> cannot afford to have misbehave.

This repository holds the releases and the changelog. The source code is not public.

## Download

Get the installer from [Releases](https://github.com/mazduino/mazduino-tuner/releases):
`MazduinoTuner-Setup-<version>.exe`.

- Windows 10 or 11, 64-bit
- No administrator rights needed: it installs for the current user
- A Mazduino ECU on USB (other rusEFI boards and Speeduino can be opened too)

### "Windows protected your PC"

Alpha builds are not code-signed yet, so Windows SmartScreen warns before the installer runs.
Click **More info**, then **Run anyway**. Check that the file came from this repository's
Releases page; each release lists its SHA-256.

## What it does

- Connects over USB serial and reads the ECU's own definition (INI), so every menu page matches
  the firmware on the board
- Menus grouped by engine subsystem, with search
- Table and curve editors with a live pointer, block edits and undo
- Changes go to ECU RAM first and are saved with **Burn**; writing is off until you allow it
- `.mdt` tune projects, plus TunerStudio `.msq` import, export and compare
- Data logger that always records, with `.mlg` / `.csv` save and open
- Real Time view of every output channel
- VE autotune, diagnostics, trigger logger, CAN analyzer
- **Firmware update**: writes a published [mazduino-fw](https://github.com/mazduino/mazduino-fw)
  build (or your own `.bin` / `.hex`) over USB, with no BOOT0 jumper. The current tune is saved
  as `.msq` first.
- Indonesian and English interface, dark and light themes

## Where your files are

| What | Where |
|---|---|
| Settings, connection and firmware-update logs, tune backups | `%APPDATA%\MazduinoTuner` |
| Data logs | `Documents\Mazduino Tuner\Logs`, or beside the `.mdt` project |

Uninstalling leaves these in place.

## Reporting a problem

Open an [issue](https://github.com/mazduino/mazduino-tuner/issues) with:

- the Mazduino Tuner version (title bar / installer name) and the ECU firmware (shown in the toolbar)
- what you did and what happened
- `%APPDATA%\MazduinoTuner\connection.log` for connection problems, or
  `%APPDATA%\MazduinoTuner\firmware-update.log` for firmware updates

## License

Mazduino Tuner is free to use. It is not open source; all rights reserved by Mazduino.

It ships third-party tools for firmware updates, listed in `tools\THIRD_PARTY_NOTICES.txt` in
the install folder: dfu-util (GPL-2.0, source at https://dfu-util.sourceforge.net/) and
STMicroelectronics' STM32 bootloader USB driver.
