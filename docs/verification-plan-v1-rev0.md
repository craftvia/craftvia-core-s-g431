# CraftVia Core-S G431 v1 Rev0 Verification Plan

> Status: Draft plan for unverified Rev0 hardware. A listed test is not a test result.

Record board ID, assembly date, BOM deviations, instruments, firmware commit, option bytes, test operator, and evidence for every run. Mark each item Pass, Fail, Blocked, or Not run.

| ID | Test | Pass criteria |
| --- | --- | --- |
| `CSG431-R0-001` | Release identity and SHA-256 | Board, source, BOM, and Gerber identify v1 Rev0; frozen assets match `SHA256SUMS.txt`. |
| `CSG431-R0-002` | Visual and mechanical inspection | Orientation, joints, DNP sites, outline, headers, and keying have no visible defect. |
| `CSG431-R0-003` | Unpowered rail checks | No short on VDD/VDDA/VBAT/GND; default V0 links match the BOM. |
| `CSG431-R0-004` | Current-limited first power | Stable 3.3 V input, no current-limit event, abnormal heat, smoke, or odor. |
| `CSG431-R0-005` | SWD/reset/flash recovery | Device ID, halt, erase, program, verify, reset, and connect-under-reset succeed repeatedly. |
| `CSG431-R0-006` | BOOT0 | N4 selects system-memory boot without contention or loss of SWD recovery. |
| `CSG431-R0-007` | Clock and 170 MHz operation | Configured clocks start reliably; frequency, current, and temperature are recorded. |
| `CSG431-R0-008` | USB | Enumeration, transfer, reset, reconnect, and recovery work through the intended Station-S path. |
| `CSG431-R0-009` | Core-S contacts | Every N/E/S/W contact maps correctly and adjacent contacts are isolated. |
| `CSG431-R0-010` | UART/I2C/SPI/timers | Representative profile functions pass with expected pin mapping. |
| `CSG431-R0-011` | ADC/DAC/analog | Channel mapping, offset, noise, and representative conversions are recorded. |
| `CSG431-R0-012` | Optional profiles | FDCAN, external VBAT, HSE, and LSE are tested only on explicitly recorded populations. |

Stop immediately for unexpected heating, unstable supply, current limiting, reversed orientation, or signal-driver contention. Rev0 may be marked verified only after mandatory tests pass on an identified production-representative assembly and the evidence is published.
