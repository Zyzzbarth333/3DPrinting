# 3d-printing-configs

Configuration for my 3D printing setup: the live Klipper stack for a modded
Ender 3 V2, an earlier config for the same printer's previous mainboard, and
SuperSlicer filament profiles.

## Printer

Modded **Ender 3 V2** (235 x 235 bed) running Klipper. The mainboard has been
upgraded once, so there are two Klipper configs here, kept separate by board.

### Current: BTT CB1 + Manta E3 EZ

[`klipper/manta-e3ez-cb1/`](klipper/manta-e3ez-cb1) is the live setup.

| Part | Detail |
|---|---|
| Host | BIGTREETECH CB1 compute module (Allwinner SoC, not a Raspberry Pi) |
| Mainboard | BIGTREETECH Manta E3 EZ (STM32G0B1) |
| Drivers | TMC2209 over UART, calibrated rotation_distance 40.115 (X/Y) |
| Probe | BLTouch / CR Touch, with bed_mesh and safe_z_home |
| Z | Dual Z with z_tilt |
| Input shaping | ADXL345 on the host MCU, input_shaper calibrated |
| Stack | Klipper, Moonraker, Mainsail, Crowsnest, Sonar, moonraker-timelapse |

| File | Holds |
|---|---|
| `printer.cfg` | Kinematics, drivers, probe, z_tilt, input shaper, macros |
| `mainsail.cfg` | Mainsail-managed section (park positions, defaults) |
| `moonraker.conf` | Moonraker server, authorization, update_manager |
| `crowsnest.conf` | Webcam streamer |
| `sonar.conf` | Network keepalive |
| `timelapse.cfg` | moonraker-timelapse settings |
| `firmware/klipper_build.config` | menuconfig used to build the STM32G0B1 MCU firmware |

Custom macros include START_PRINT, END_PRINT, PURGE_LINE, M600 / CHANGE_FILAMENT,
BED_TRAM, G29 (bed mesh), G34 (z_tilt), Z_OFFSET, and pause / resume / cancel.

### Previous: Raspberry Pi + SKR V1.4

[`klipper/skr1.4-pi/printer.cfg`](klipper/skr1.4-pi/printer.cfg) is the earlier
config, for a BIGTREETECH SKR V1.4 (LPC1768) hosted on a Raspberry Pi. Kept for
reference; it is not the current setup.

## Deploying

Drop the files from the relevant board folder into `~/printer_data/config/` on
the host, then adjust anything host-specific (the `virtual_sdcard` path, the
`[mcu]` serial). Klipper requires the MCU firmware to match the host Klipper
version, so rebuild MCU firmware for the board rather than reusing an old binary.
`klipper_build.config` is the menuconfig reference for the Manta E3 EZ build.

## SuperSlicer filament profiles

In [`superslicer/filament/`](superslicer/filament). Import each from
SuperSlicer's Filament Settings tab.

| Filament | Type | Nozzle (first / print) | Bed (first / print) |
|---|---|---|---|
| Polymaker PolyLite PLA+ Pro | PLA | 220 / 215 °C | 50 / 50 °C |
| Polymaker PolyLite ABS | ABS | 250 / 245 °C | 70 / 85 °C |
| Polymaker PolyFlex TPU90 | TPU | 220 / 220 °C | 60 / 60 °C |

Print and system settings are not included.

## Licence

Released under The Unlicense. See [`LICENSE`](LICENSE).
