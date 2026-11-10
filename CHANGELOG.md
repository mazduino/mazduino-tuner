# Changelog

Versions follow `major.minor.patch`; `-alpha.N` and `-beta.N` are test builds.

## Unreleased

### New
- The app knows each ECU. If you open a project and connect to a different ECU (for example
  another car with the same board), it warns you first: **Cancel** keeps the project offline and
  changes nothing, **Continue** compares the tunes as usual. Keeping that ECU's tune never
  overwrites the other car's project
- When you save a new project, the app asks for a vehicle name (you can skip it)
- The Start page shows the hardware, a short hardware serial, the firmware and the vehicle name

### Fixed
- Sending a project's tune to an ECU no longer copies the other ECU's internal ID into it

## 0.1.0-alpha.1 — 2026-11-08, installer updated 2026-11-11

The installer on the release page was replaced on 11 November 2026. It has everything below. The
first download (8 November) had only the "First public test build" part; download it again to get
the rest.

### New in the 11 November installer
- The app tells you when a new version is out (toolbar and Start page), with the changes and a
  download link
- Each test build works for a limited time (this one until 11 December 2026). The last week is
  shown in the toolbar; after that the app only offers the new version. Your tunes, logs and
  settings are kept
- The Start page shows the app version and works without an ECU
- Edit a project offline; when you connect, the differences with the ECU are shown side by side
  with large, clear buttons to choose which tune to use
- Projects from older firmware are compared setting by setting and are never overwritten by a
  tune they cannot hold
- After a firmware update the app checks the tune and shows what changed
- Right-click a menu page to load just that page from a file, give it a function key or add it
  to the Shortcuts tab
- Choose which channels the Real Time tab shows
- The window title shows the version, connection, open project and firmware
- The trigger page draws the selected trigger wheel
- Turn the Logger graph off with **Graph off** to keep the app light; recording carries on
- The status bar shows when the trigger logger, trigger sniffer, trigger scope or VE autotune is
  running, and the app asks before you leave a running trigger tool
- Works with official rusEFI and other rusEFI-based firmware too, with their own page names
- Project files (.mdt) carry the ECU definition, so they open on any PC without internet
- The installer also installs the USB driver needed for firmware updates (once, if missing)

### Improved
- Tables fit on screen in full above the bottom panel
- Much lighter on the PC during live data, especially with large tables and the trigger tools;
  almost no load when the window is in the background. The ECU is asked only for the values on
  screen, so it works less too
- Trigger logger and sniffer graphs fit the window and are easier to read
- Reads every TunerStudio project (.msq)
- Menus and pages respond faster
- Calmer table colours, a neutral grey for the selected row
- Table axes show their real names and units
- Pages for features that are turned off are hidden until you turn the feature on
- Fuel pressure sensor is now under Inputs › Sensors
- Menus stay up to date for every firmware version
- English is the default language (Indonesian is in Settings)
- Trigger sniffer starts when you press Start
- Settings and the status bar no longer show internal folder paths

### Fixed
- A "polling failed" message could stay on screen after the link had recovered
- The Logger graph went blank when the cursor was past the end of the log
- Custom trigger wheels could show merged teeth
- Some tables (injector dead time, cranking fuel) were shown the wrong way round
- Closing the app while connected could lose the data log
- After a firmware update the app sometimes could not reconnect

### First public test build (8 November)

#### Connection
- USB serial link to Mazduino ECUs (rusEFI), with auto-connect when the ECU is plugged in
- Recovers the link by itself after a USB stall, keeping the tune and unsent edits
- Opens official rusEFI boards, custom firmware and Speeduino as well
- Data rate setting for live data

#### Tuning
- Every menu page built from the ECU's INI, grouped by engine subsystem, with search
- Table editor: live pointer with trail, block edits, undo/redo, cell locking
- Curve editor, including editing the axis values
- Writes go to ECU RAM and are saved with Burn; writing must be allowed per connection
- Tracks changes that are sent but not burned
- Display units: °C/°F, kPa/psi, lambda/AFR

#### Tune files
- `.mdt` projects, compared with the ECU when connecting
- TunerStudio `.msq` import, export and compare

#### Logging and analysis
- Always-on data logger, `.mlg` / `.csv` save and open, cursor linked to tables
- Real Time view of all output channels, grouped like the INI
- VE autotune from live data or a log
- Diagnostics: error codes, tune problems, cylinder shutoff, trigger logger and scope
- CAN analyzer on the firmware's text console

#### Firmware
- Firmware update from published mazduino-fw releases or a `.bin` / `.hex` file
- Board check against the ECU's signature; nightly builds need an extra confirmation
- Sends the ECU into the STM32 bootloader with `reboot_dfu`, writes with dfu-util, reconnects
- Installs the STM32 bootloader USB driver when Windows has none (one permission prompt)
- Saves the current tune as `.msq` before writing

#### Known issues
- Not code-signed yet: Windows SmartScreen asks for **More info → Run anyway**
- On some PCs the USB link drops for a second now and then (Windows error 995); the app
  reconnects by itself
- Driver installation for the STM32 bootloader has not been tested on a PC without the driver
