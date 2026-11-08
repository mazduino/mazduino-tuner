# Changelog

Versions follow `major.minor.patch`; `-alpha.N` and `-beta.N` are test builds.

## 0.1.0-alpha.1 — 2026-11-08

First public test build.

### Connection
- USB serial link to Mazduino ECUs (rusEFI), with auto-connect when the ECU is plugged in
- Recovers the link by itself after a USB stall, keeping the tune and unsent edits
- Opens official rusEFI boards, custom firmware and Speeduino as well
- Data rate setting for live data

### Tuning
- Every menu page built from the ECU's INI, grouped by engine subsystem, with search
- Table editor: live pointer with trail, block edits, undo/redo, cell locking
- Curve editor, including editing the axis values
- Writes go to ECU RAM and are saved with Burn; writing must be allowed per connection
- Tracks changes that are sent but not burned
- Display units: °C/°F, kPa/psi, lambda/AFR

### Tune files
- `.mdt` projects, compared with the ECU when connecting
- TunerStudio `.msq` import, export and compare

### Logging and analysis
- Always-on data logger, `.mlg` / `.csv` save and open, cursor linked to tables
- Real Time view of all output channels, grouped like the INI
- VE autotune from live data or a log
- Diagnostics: error codes, tune problems, cylinder shutoff, trigger logger and scope
- CAN analyzer on the firmware's text console

### Firmware
- Firmware update from published mazduino-fw releases or a `.bin` / `.hex` file
- Board check against the ECU's signature; nightly builds need an extra confirmation
- Sends the ECU into the STM32 bootloader with `reboot_dfu`, writes with dfu-util, reconnects
- Installs the STM32 bootloader USB driver when Windows has none (one permission prompt)
- Saves the current tune as `.msq` before writing

### Known issues
- Not code-signed yet: Windows SmartScreen asks for **More info → Run anyway**
- On some PCs the USB link drops for a second now and then (Windows error 995); the app
  reconnects by itself
- Driver installation for the STM32 bootloader has not been tested on a PC without the driver
