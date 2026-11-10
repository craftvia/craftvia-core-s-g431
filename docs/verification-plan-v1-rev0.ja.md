# CraftVia Core-S G431 v1 Rev0 検証計画

> 状態: 未検証Rev0向けのDraft計画です。項目の記載は試験合格を意味しません。

Board ID、実装日、BOM差分、測定器、Firmware commit、Option bytes、実施者、Evidenceを記録し、各項目をPass / Fail / Blocked / Not runで判定します。

| ID | 試験 | 合格基準 |
| --- | --- | --- |
| `CSG431-R0-001` | Release識別とSHA-256 | Board、Source、BOM、Gerberがv1 Rev0を示し、凍結資産がmanifestと一致する。 |
| `CSG431-R0-002` | 外観・機械確認 | 向き、はんだ、DNP、外形、Header、Keyに異常がない。 |
| `CSG431-R0-003` | 未通電電源確認 | VDD/VDDA/VBAT/GNDに短絡がなく、V0実装がBOMと一致する。 |
| `CSG431-R0-004` | 電流制限付き初回通電 | 3.3 Vが安定し、電流制限、異常発熱、発煙、異臭がない。 |
| `CSG431-R0-005` | SWD/Reset/Flash recovery | ID読出し、halt、erase、program、verify、reset、connect-under-resetが反復成功する。 |
| `CSG431-R0-006` | BOOT0 | N4でSystem memory bootへ入り、Driver競合やSWD recovery喪失がない。 |
| `CSG431-R0-007` | Clock/170 MHz | Clockが安定起動し、周波数、電流、温度を記録できる。 |
| `CSG431-R0-008` | USB | Station-S経路でenumeration、transfer、reset、reconnect、recoveryが成功する。 |
| `CSG431-R0-009` | Core-S全接点 | N/E/S/W全接点のMappingと隣接絶縁が正しい。 |
| `CSG431-R0-010` | UART/I2C/SPI/Timer | 代表Profileが期待したPin mappingで動作する。 |
| `CSG431-R0-011` | ADC/DAC/Analog | Channel、offset、noise、代表変換結果を記録する。 |
| `CSG431-R0-012` | Option profile | FDCAN、外部VBAT、HSE、LSEを明示した実装構成だけで試験する。 |

異常発熱、電源不安定、電流制限、逆挿し、Signal driver競合があれば直ちに停止します。Mandatory testが識別済みの製造代表個体で合格し、Evidenceを公開するまでVerifiedと表示しません。
