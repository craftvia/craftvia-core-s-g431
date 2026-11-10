# CraftVia Core-S G431 v1 Rev0 リリースノート（参考訳・要約）

英語版 [`RELEASE_NOTES.md`](RELEASE_NOTES.md) を正本とします。

- Freeze: 2026-10-26 22:35 JST
- 状態: 初回Prototype基板製造向けに凍結、基板発注済み・到着待ち、未実装・未検証
- 標準実装: `P10 + V0 + C0`
- PCB: 25.40 mm角、4層、公称1.60 mm
- PCB DRC: Error 0 / Warning 0
- 原理図DRC: Fatal 0 / Error 0 / Warning 2（Supplier属性正規化警告）
- 製造正本: `fabrication/Gerber_PCB1_2026-11-04.zip`
- 実装正本: BOM。CPLは標準実装23 designatorへFilter済み

旧staging manifestにはGerberのPathとDigestに不整合がありました。公開用 `SHA256SUMS.txt` は実在する2026-11-04 GerberのDigestへ訂正しています。Gerber本体は変更していません。

発注前に英語正本のStack-up、USB 90 ohm差動、Population option、初品検証項目を確認してください。
