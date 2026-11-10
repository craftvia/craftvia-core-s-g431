# CraftVia Core-S G431 v1 Rev0 Specification

> [!WARNING]
> **Frozen design, unverified hardware.** This document describes the Rev0 implementation; it does not claim verified Core-S conformance.

## Identity and authority

| Item | Value |
| --- | --- |
| MCU | STM32G431CBT6, LQFP48 |
| PCB | 25.4 mm × 25.4 mm, 4 layers |
| Supply | Regulated 3.3 V input |
| Frozen source | `../source/CraftVia-Core-S-G431-v1-Rev0.eprj2` |
| Fabrication master | `../fabrication/Gerber_PCB1_2026-11-04.zip` |
| Default population | `P10 + V0 + C0` |

The frozen source, fabrication master, authoritative BOM, and release record control Rev0. Common requirements are defined by the [Core-S Interface v1](https://github.com/craftvia/craftvia-docs/blob/main/standards/core-s-interface-v1.md).

## Hardware summary

- Arm Cortex-M4F up to 170 MHz; 128 KiB Flash and 32 KiB SRAM.
- SWD on N1/N2/N3 and physical BOOT0 on N4.
- Native USB FS on N7/N8 with MCU-side series resistors.
- ADC, DAC, op-amps, comparators, timers, UART, I2C, SPI, and profile-dependent FDCAN access.
- No onboard input regulator or general-purpose input protection; the host supplies a suitable 3.3 V rail.

## Core-S contact mapping

| Contact | MCU signal | Package pin | Representative role |
| --- | --- | ---: | --- |
| N1 | PG10-NRST | 7 | Active-low reset |
| N2 | PA13 | 37 | SWDIO |
| N3 | PA14 | 38 | SWCLK |
| N4 | PB8-BOOT0 | 45 | Physical BOOT0 request |
| N5 | PA15 | 39 | Debug auxiliary / GPIO |
| N6 | PB3 | 40 | SWO / GPIO |
| N7 | PA11 | 33 | USB DM or FDCAN RX by profile |
| N8 | PA12 | 34 | USB DP or FDCAN TX by profile |
| E1-E8 | PA0-PA7 | 8-15 | ADC and mixed-signal group |
| S1 | PA8 | 30 | TIM1_CH1 |
| S2 | PB0 | 16 | ADC/timer |
| S3 | PB1 | 17 | ADC/timer |
| S4 | PB9 | 46 | FDCAN/I2C/UART/GPIO |
| S5-S8 | PB12-PB15 | 26-29 | SPI2/timer/GPIO group |
| W1-W2 | PA9/PA10 | 31/32 | USART1 pair |
| W3-W4 | PB10/PB11 | 22/25 | UART/ADC-capable pair |
| W5-W8 | PB4-PB7 | 41-44 | SPI1/GPIO group |

`K-SW` is the 3.3 V input. `K-NW` and `K-NE` are GND. Alternate-function use must be checked against the STM32G431 datasheet and the selected firmware profile.

## Default configuration

- `P10`: N7/N8 are USB DM/DP; N4 remains physical BOOT0.
- `V0`: SJ1 is fitted; D1 and J8 are DNP; `VBAT_BACKUP` follows `VDD_CORE`.
- `C0`: HSE/LSE parts are DNP; firmware uses HSI16 + PLL and HSI48 + CRS for USB.
- Do not use N7/N8 for USB and FDCAN simultaneously.
- For external VBAT, remove SJ1 before fitting D1/J8. Never apply an external primary cell while SJ1 is fitted.

## Manufacturing constraints

- Four-layer JLC04161H-7628 baseline, nominal 1.60 mm.
- USB target is 90 ohm differential, ±10% manufacturing tolerance; confirm against the selected production stack-up.
- Gerber is the fabrication master. BOM controls population; the filtered CPL contains the 23 standard populated designators.
- Preserve the frozen manufacturing assets and create a new PCB revision for electrical, footprint, routing, silkscreen, or population changes.

## Known unverified areas

USB through the full Core-S/Station-S path, FDCAN, external VBAT, HSE/LSE startup, ADC accuracy, current consumption, thermal behavior, and continuous 170 MHz operation require first-article validation.
