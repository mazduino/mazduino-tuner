# Changelog

Versions follow `major.minor.patch`; `-alpha.N` and `-beta.N` are test builds.

## Unreleased

### New
- Turn the Logger graph off with **Graph off** to keep the app light; recording carries on
- The status bar shows when the trigger logger, trigger sniffer, trigger scope or VE autotune is
  running, and the app asks before you leave a running trigger tool
- Works with official rusEFI and other rusEFI-based firmware too, with their own page names
- Project files (.mdt) now carry the ECU definition, so they open on any PC without internet
- The installer also installs the USB driver needed for firmware updates (once, if missing)

### Improved
- The app stays smoother during live data, especially on pages with large tables, and asks the
  ECU only for the values on screen, so both work less
- Menus and pages respond faster
- Calmer table colours that are easier on the eyes
- Table axes show their real names and units
- Pages for features that are turned off are hidden until you turn the feature on
- Fuel pressure sensor is now under Inputs › Sensors
- Menus stay up to date for every firmware version
- English is the default language (Indonesian is in Settings)
- Trigger sniffer starts when you press Start

### Fixed
- Some tables (injector dead time, cranking fuel) were shown the wrong way round
- Closing the app while connected could lose the data log
- After a firmware update the app sometimes could not reconnect

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
