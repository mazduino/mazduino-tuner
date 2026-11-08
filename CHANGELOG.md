# Changelog

Versions follow `major.minor.patch`; `-alpha.N` and `-beta.N` are test builds.

## Unreleased

### Changed
- English is the default interface language; Indonesian stays available in Settings, and a
  language already chosen is kept
- The Start page shows the board, port and firmware only, without the paths of the ECU
  definition files
- Trigger sniffer starts only when you press Start, and drops data the ECU recorded before that
- While the trigger logger, trigger sniffer or trigger scope runs, the status bar shows it, and
  opening another page asks first: leaving stops it
- The Logger tab's live chart can be turned off with **Graph on/off** to save CPU; recording
  goes on and opened log files are still drawn (on the test laptop: about 62 % → 15 % of one
  CPU core)
- Live data defaults to 50 reads per second and never goes above 100, so the ECU stays light
  (about 6 % of its CPU at 100/s, a third of it when read as fast as possible); 200 and "Max"
  from older settings become 100
- Tables use calmer colours with smaller steps between values; curves are plain rows
- Table axes are named as the firmware names them, with units (e.g. Battery (volts),
  Pressure (kPa))
- Menu pages whose feature is turned off are hidden until it is turned on
- Fuel pressure sensor is under Inputs › Sensors; Trailing ignition (rotary) moved to Expert
- Menus follow layout updates for firmware of every date, not only the newest
- The status bar shows when VE autotune is running
- ECU command buttons (e.g. the trigger stimulator) say they need "Allow writes"

### Fixed
- Tables that are not square (injector dead time, cranking base fuel, …) were drawn with rows
  and columns swapped
- Closing the window now disconnects first, as the Disconnect button does: the running data log
  (over 30 s) is saved, the CAN console is turned off and the serial port is closed. Before, the
  log was lost when the app was closed while connected.

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
