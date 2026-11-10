# CraftVia Core-S G431 v1 Rev0 仕様書

> [!WARNING]
> **凍結済み設計・未検証ハードウェアです。** 本書はRev0実装を記述しますが、Core-S適合の実機検証完了を示すものではありません。

## 識別と正本

| 項目 | 内容 |
| --- | --- |
| MCU | STM32G431CBT6、LQFP48 |
| PCB | 25.4 mm × 25.4 mm、4層 |
| 電源 | 安定化済み3.3 V入力 |
| 凍結済みSource | `../source/CraftVia-Core-S-G431-v1-Rev0.eprj2` |
| 製造正本 | `../fabrication/Gerber_PCB1_2026-11-04.zip` |
| 標準実装 | `P10 + V0 + C0` |

凍結済みSource、Gerber、BOM、Release recordをRev0の正とします。共通要件は[Core-S Interface v1](https://github.com/craftvia/craftvia-docs/blob/main/standards/core-s-interface-v1.md)を参照してください。

## ハードウェア概要

- Arm Cortex-M4F、最大170 MHz、Flash 128 KiB、SRAM 32 KiB。
- N1/N2/N3にSWD、N4に物理BOOT0。
- N7/N8にNative USB FS。ProfileによりFDCANと排他。
- E1-E8にPA0-PA7、W1/W2にUSART1、W5-W8にSPI1の代表配置。
- Core上に入力Regulatorや一般的な入力保護はなく、Hostが適切な3.3 Vを供給します。

## 標準構成

- `P10`: N7/N8はUSB DM/DP、N4は物理BOOT0。
- `V0`: SJ1実装、D1/J8はDNP。`VBAT_BACKUP`は`VDD_CORE`へ追従。
- `C0`: HSE/LSE部品はDNP。HSI16 + PLL、USBはHSI48 + CRSを使用。
- N7/N8でUSBとFDCANを同時使用しないでください。
- 外部VBAT構成ではSJ1を外してからD1/J8を実装します。SJ1実装中に外部一次電池を接続しないでください。

## 製造条件

- 4層JLC04161H-7628を基準とし、公称厚さ1.60 mm。
- USBは90 ohm差動、製造公差±10%を目標とし、選択した製造Stack-upで確認します。
- GerberをPCB製造正本、BOMを実装正本とします。CPLは標準実装23 designatorへFilter済みです。
- 電気、Footprint、配線、Silkscreen、実装内容を変更する場合は新しいPCB Revisionを作成します。

## 未検証項目

Core-S/Station-S全経路のUSB、FDCAN、外部VBAT、HSE/LSE起動、ADC精度、消費電流、温度、170 MHz連続動作は初品で検証します。
