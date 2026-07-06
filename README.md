# 3D Printing

Configuration files for my 3D printing setup: a Klipper config for a modded
Ender 3 V2, and SuperSlicer filament profiles.

## Printer

Modded **Ender 3 V2** running Klipper (Mainsail):

- Hero Me Gen 7 toolhead
- Dragon HF hotend
- CR Touch bed probe
- Dual Z axis with Z-Tilt
- BIGTREETECH SKR V1.4 board (LPC1768)

## Klipper config

[`Klipper Configurations/Ender3V2modded.cfg`](Klipper%20Configurations/Ender3V2modded.cfg)
is the printer config for the setup above. It assumes a Mainsail install
(`[include mainsail.cfg]`) and the SKR 1.4 pin map. Use it as your `printer.cfg`
(or include it), then set anything host-specific such as the `virtual_sdcard`
path.

## SuperSlicer filament profiles

In [`SuperSlicer/Filament Settings/`](SuperSlicer/Filament%20Settings). Import each
from SuperSlicer's Filament Settings tab.

| Filament | Type | Nozzle (first / print) | Bed (first / print) |
|---|---|---|---|
| Polymaker PolyLite PLA+ Pro | PLA | 220 / 215 °C | 50 / 50 °C |
| Polymaker PolyLite ABS | ABS | 250 / 245 °C | 70 / 85 °C |
| Polymaker PolyFlex TPU90 | TPU | 220 / 220 °C | 60 / 60 °C |

Print settings and system settings are not included yet.
