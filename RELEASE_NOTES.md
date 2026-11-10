# CraftVia Core-S G431 v1 Rev0 Hardware Release

## Release status

- Revision: Rev0
- Freeze date: 2026-10-26 22:35 JST
- Status: FROZEN for initial prototype PCB fabrication
- Hardware status: PCB ordered; awaiting delivery, unassembled and unverified
- Intended use: Rev0 engineering prototype; not a general-production release
- Default assembly variant: `P10 + V0 + C0`
- Assembly plan: bare-PCB fabrication followed by manual assembly; no turnkey PCBA is planned for the first article
- CAD: EasyEDA Pro `v3.2.149.88089769`; frozen project database schema `25.10.31.1`
- Checked by: Kohei (design owner) and Codex (release-file consistency review)
- Authoritative editable source: `source/CraftVia-Core-S-G431-v1-Rev0.eprj2`
- Authoritative source SHA-256: `ebae7a9b5478990bd138dd12e0b18ce9bee6f9e6addf61ce0b01c9f8536e7b01`
- Authoritative PCB fabrication upload: `fabrication/Gerber_PCB1_2026-11-04.zip`

The EasyEDA Pro application build is recorded from the final Gerber export header. The portable project title and schematic title identify this release as G431. The authoritative `.eprj2` retains the historical `projects.name` value `CraftVia-Core-S-G031-v1-Rev0` as EasyEDA workflow-link metadata; this accepted metadata does not identify the released circuit or fabrication data.

## Release decision

The package is acceptable for an initial Rev0 bare-PCB fabrication order and manual first-article assembly, subject to the ordering and bring-up conditions below.

- PCB strict DRC: PASS, 0 errors and 0 warnings, as confirmed in EasyEDA before export
- Schematic DRC: Fatal 0, Error 0, Warning 2
- The two schematic warnings are EasyEDA Supplier Part attribute-normalization warnings. They cover the listed components but do not report an electrical-connectivity error.
- Gerber ZIP integrity and required layer presence: PASS
- BOM/CPL population reconciliation: PASS; 23 populated designators in both sets
- Assembly PDF: 11 pages; assembly instructions followed by the EasyEDA PCB/layer reference export
- Board: 25.40 mm x 25.40 mm, 4 copper layers, nominal finished thickness 1.60 mm

## Release contents

| Path | Purpose |
| --- | --- |
| `source/CraftVia-Core-S-G431-v1-Rev0.eprj2` | Authoritative editable EasyEDA project |
| `source/ProPrj_CraftVia-Core-S-G431-v1-Rev0_2026-10-26.epro` | Portable EasyEDA project archive |
| `fabrication/Gerber_PCB1_2026-11-04.zip` | Canonical PCB fabrication package |
| `assembly/BOM_Board1_PCB1_2026-10-26.csv` | Full BOM with explicit DNP status |
| `assembly/PickAndPlace_PCB1_2026_10_26.csv` | EasyEDA CPL export containing the 23 populated designators |
| `assembly/CraftVia-Core-S-G431-v1-Rev0-Assembly.pdf` | Top/Bottom assembly instructions and PCB reference pages |
| `docs/SCH_Core-S-G431-v1-Rev0_2026-10-26.pdf` | Human-readable schematic reference |
| `SHA256SUMS.txt` | Per-file SHA-256 integrity manifest |

The three files under `img/` are convenience renderings only. They are intentionally retained for visual reference but are not release masters and are excluded from `SHA256SUMS.txt`. DRC log files are intentionally not frozen; the accepted DRC results and warning disposition are recorded in this README.

## PCB fabrication package

Upload `fabrication/Gerber_PCB1_2026-11-04.zip` directly to the PCB manufacturer. Do not edit or recompress its contents.

The ZIP contains:

- Top, Inner 1, Inner 2 and Bottom copper
- Top and Bottom solder mask
- Top and Bottom silkscreen
- Top paste mask
- Top assembly and document layers
- Board outline
- PTH component-hole drill and PTH via drill

No NPTH drill file is present. No Bottom paste file is present because the standard populated SMT parts are on the Top side.

Order and stack-up conditions:

- Manufacturer baseline: JLCPCB
- Stack-up: `JLC04161H-7628`
- Finished thickness: nominal 1.60 mm, subject to manufacturer tolerance
- Copper: L1/L4 1 oz; L2/L3 0.5 oz
- L1-L2 and L3-L4 dielectric: `7628 RC49% 8.6 mil`
- L2-L3 core: `1.1 mm H/HOZ Copper`
- USB pair: L1 non-coplanar differential microstrip over continuous L2 GND
- USB differential impedance: 90 ohm, manufacturing tolerance +/-10%
- USB routing rule: 0.2474 mm width, 0.1524 mm pair gap, intra-pair mismatch no more than 0.5 mm
- Surface finish and solder-mask color are not encoded in Gerber. Select them explicitly when ordering and record them when the release status is updated to `ORDERED`.

Before submitting the order, load the exact ZIP into the manufacturer preview and confirm the 25.40 mm square outline, four copper layers, stack-up selection, impedance requirement, plated header/test-point holes, solder-mask openings, silkscreen, and drill alignment.

## Assembly population

The BOM contains 29 rows and 33 component designators. DNP options remain in the BOM with `DNP=Yes` so a fresh export preserves the implementation choice.

Standard populated designators for `P10 + V0 + C0`:

`C1, C2, C3, C4, C5, C6, C7, C8, C13, C14, J1, J2, J3, J4, J5, J6, J7, R1, R2, R4, R5, SJ1, U1`

Intentional DNP designators:

`C9, C10, C11, C12, D1, J8, R3, R6, X1, X2`

Test points excluded from BOM/CPL population:

`TP1, TP2, TP3, TP4, TP5, TP6`

The filtered CPL contains exactly the 23 standard populated designators and excludes all ten DNP components and all six test points. Because the first article will not use turnkey PCBA, the CPL is retained for coordinate, side and rotation audit only. All assembly is manual; no parts are assigned to an external assembler for this build.

## Default electrical and implementation configuration

- Communication profile `P10`: N7/N8 are USB DM/DP; N4 remains physical BOOT0; R4 = 1 kohm and R5 = 10 kohm are fitted.
- VBAT option `V0`: SJ1 = 0 ohm fitted; D1 and J8 DNP; `VBAT_BACKUP` follows `VDD_CORE`.
- Clock option `C0`: X1, R6, C9, C10, X2, C11 and C12 are DNP; use HSI16 + PLL and HSI48 + CRS for USB.
- R3 is DNP in every standard Rev0 variant.
- External VBAT option `V1`: remove SJ1 before fitting D1 and J8. D1 anode faces J8 and cathode faces `VBAT_BACKUP`. Never fit SJ1 and apply an external primary cell through J8 simultaneously.
- USB and FDCAN share profile-dependent pins. Do not use N7/N8 for USB and FDCAN simultaneously. The P30 profile moves FDCAN to N4/PB8 and S4/PB9 and requires the documented BOOT option-byte and Station-side isolation conditions.

## DRC and documentation evidence

Schematic DRC was run before export and reported Fatal 0, Error 0 and Warning 2. The warnings are accepted because they concern supplier-attribute normalization rather than connectivity. PCB strict DRC was run after copper rebuild and reported zero errors and zero warnings. Both results were confirmed in EasyEDA before the release exports were collected. DRC logs are not part of this frozen package.

The schematic and assembly PDFs are human-readable references. The Gerber ZIP is the sole PCB fabrication master. BOM population status controls assembly, and the filtered CPL must not be expanded with DNP or test-point rows for an assembly order.

## First-article checks

1. Verify the order preview against the specified four-layer stack-up and 90-ohm USB differential requirement.
2. Inspect header orientation, pin 1, U1 pin 1 and all polarity markings before power is applied.
3. Confirm SJ1 is fitted and D1/J8 are not fitted for the default `V0` assembly.
4. Power from a current-limited 3.3 V source and confirm no short between `VDD_CORE`, `VDDA_REF`, `VBAT_BACKUP` and GND.
5. Verify SWD connection, NRST operation, flash erase/write/verify and recovery behavior.
6. Verify physical BOOT0 operation for P10 and record the released option-byte values.
7. Exercise all Core-S edge signals and TP1-TP6 with a continuity fixture or Station-S.
8. Validate USB through the Core-S and Station-S interconnect; the Station-side path must also satisfy the 90-ohm differential requirement.
9. Measure 170 MHz operation, current and temperature before claiming full-speed continuous operation.
10. Treat HSE, LSE, external VBAT, FDCAN and precision analog performance as optional functions requiring their own populated variant and bench validation.

## Known limitations

- This is an engineering prototype release. USB signal integrity through the complete Core-S/Station-S path, FDCAN, external VBAT, HSE/LSE startup, ADC accuracy, power consumption and thermal behavior remain first-article validation items.
- Surface finish and solder-mask color remain order-time selections and must be recorded when an order is placed.
- Regeneration should use EasyEDA Pro `v3.2.149.88089769` where practical; a different build must be recorded if a later repack is required.
- The historical `.eprj2` workflow-link name is intentionally accepted for Rev0. Circuit, schematic, PCB and portable-project titles identify G431.

## Change control and integrity

Verify each listed release file with `SHA256SUMS.txt` before ordering. The manifest records one SHA-256 digest per file and does not represent a directory-level digest. `SHA256SUMS.txt` does not hash itself. The three convenience images under `img/` and all DRC logs are outside the integrity manifest.

After this release is used for an order, do not overwrite any Rev0 file. Electrical, footprint, routing, silkscreen or population changes require a new revision. A documentation-only repack must preserve the `.eprj2` hash and use a separately named release directory.
