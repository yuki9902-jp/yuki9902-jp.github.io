---
title: "ASUS ROG STRIX X570-F Gaming BIOS 2606 Update"
date: 2020-08-19T10:40:25+09:00
archives: ["2020-08"]
original_url: https://ameblo.jp/yuki9902/entry-12618834586.html
categories: ['COMPUTER']
---

[ASUS ROG STRIX X570-F GAMING BIOS 2606](https://www.asus.com/jp/Motherboards/ROG-Strix-X570-F-Gaming/HelpDesk_Download/)

2602が取り下げになって、2606が公開されました。

"Improve system performance and stability

Improve Fan control function

Improve DRAM stability

Update AM4 AGESA combo V2 PI 1.0.8.0

Improve system stability

Improve DRAM performance

Before running the USB flashback tool，please rename the BIOS file (SX570FG.CAP) using BIOSRenamer"

システムの性能と安定性の改善

ファンコントロール機能の改善

メモリーの安定性の改善

AM4 AGESA combo V2 PI 1.0.8.0の更新

システムの安定性の改善

メモリーの性能の改善

更新内容はBIOS 2602と変わらないように見えます。

取り下げてバージョンが少し上がっているのは何かしら変更点があったんでしょうが、ソースコード上の細かい問題でしょうかね。

さて、BIOS 2602からBIOS 2606に更新しました。

設定項目は初期化されます。

FANの端子がいくつか使い物にならなくなっていたので、CPUクーラー以外はCorsair Commander Proに統合させてしまったので、何が変わったかは見ていません。

もしかしたらFANの端子が復活しているかもしれないですが、今更面倒です。

とりあえず、XMP2に該当するD.O.C.PをDDR4-3600にして、手動でtRCを64に設定、3700Xのクロック倍率を43にして、電源周りの設定をして、Windows 10を起動させました。

特に問題はないようです。