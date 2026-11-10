# CraftVia Core-S G431

> [!WARNING]
> **Unverified Rev0 hardware**
>
> Rev0 PCBs have been ordered and are awaiting delivery. They have not yet been assembled, powered, or electrically verified. Assembly and use are at your own risk, and a later revision may change the design.

[日本語](README.ja.md) · [CraftVia](https://craftvia.org) · [Rev0 release notes](RELEASE_NOTES.md)

![CraftVia Core-S G431 v1 Rev0 CAD rendering](docs/images/3D_PCB1_2026-10-26.png)

*Rev0 CAD rendering — [front](docs/images/2D_PCB1_front_2026-10-26.png) · [back](docs/images/2D_PCB1_back_2026-10-26.png). Images are illustrative; the frozen EasyEDA source and Gerber package are authoritative.*

CraftVia Core-S G431 is a Core-S v1 implementation based on the STM32G431CBT6. It provides a 170 MHz Cortex-M4F MCU, SWD, native USB, flexible analog/timer interfaces, and optional FDCAN profiles in the 25.4 mm square Core-S form factor.

## Current status

| Item | Status |
| --- | --- |
| Product generation | v1 |
| PCB revision | Rev0 |
| Design | Frozen for initial prototype fabrication |
| PCB fabrication | Ordered; awaiting delivery |
| Assembly | Not started |
| Hardware verification | Not started |
| Release tag | `v1-rev0` planned |

## Rev0 summary

- MCU: STM32G431CBT6, LQFP48
- CPU: Arm Cortex-M4F, up to 170 MHz
- Memory: 128 KiB Flash, 32 KiB SRAM
- PCB: 25.4 mm × 25.4 mm, 4 layers
- Supply: regulated 3.3 V input
- Debug: SWD; physical BOOT0 on N4
- USB: native USB FS on N7/N8
- Default clock profile: HSI16 + PLL and HSI48 + CRS; HSE/LSE options are DNP
- CAD source: EasyEDA

The common mechanical and electrical requirements are maintained in the [CraftVia common documentation](https://github.com/craftvia/craftvia-docs). Product-specific behavior and acceptance testing are described in the Rev0 [specification](docs/specification-v1-rev0.md) and [verification plan](docs/verification-plan-v1-rev0.md).

## Repository layout

```text
source/          Authoritative editable EasyEDA sources
fabrication/     Canonical Gerber package
assembly/        BOM, filtered CPL, and assembly reference
docs/            Schematic, images, specification, and verification plan
product.json     Machine-readable public product metadata
RELEASE_NOTES.md Detailed frozen-release record
SHA256SUMS.txt   Integrity manifest for frozen manufacturing assets
```

## Important manufacturing notes

- Use `fabrication/Gerber_PCB1_2026-11-04.zip` as the PCB fabrication master.
- Select the documented four-layer stack-up and verify the 90-ohm USB differential requirement with the manufacturer.
- The default population is profile `P10 + V0 + C0`; read the release notes before changing USB/FDCAN, VBAT, or clock options.
- Verify the frozen manufacturing files against `SHA256SUMS.txt` before ordering.
- The publication manifest corrects the path and digest of the Gerber file from the earlier staging manifest; the Gerber bytes themselves are unchanged.

## License and brand

Hardware design files are licensed under [CERN-OHL-P-2.0](LICENSE), unless a file-specific notice says otherwise. Documentation and software category boundaries are described in [CraftVia Licensing](LICENSES/README.md).

The CraftVia name and logos are not licensed under the hardware license. See the [CraftVia Trademark Policy](LICENSES/TRADEMARK_POLICY.md). Modified or third-party-manufactured hardware must not be presented as an official CraftVia product.
