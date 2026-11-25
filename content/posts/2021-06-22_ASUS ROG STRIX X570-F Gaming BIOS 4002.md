---
title: "ASUS ROG STRIX X570-F Gaming BIOS 4002"
date: 2021-06-22T09:42:52+09:00
archives: ["2021-06"]
original_url: https://ameblo.jp/yuki9902/entry-12682077444.html
categories: ['COMPUTER']
---

ASUS ROG STRIX X570-F GamingのBIOS 4002が公開されました。

[ROG Strix X570-F Gaming | ROG Strix | Gaming マザーボード｜ROG - Republic of Gamers｜ROG 日本PCIe 4.0、Aura Sync RGBライティング、Intel Gigabitイーサネット、ヒートシンク付きデュアルM.2、SATA 6Gbps、およびUSB 3.2 Gen 2を搭載したAMD X570 ATXゲーミングマザーボード!rog.asus.com![](https://dlcdnwebimgs.asus.com/gain/)](https://rog.asus.com/jp/motherboards/rog-strix/rog-strix-x570-f-gaming-model/helpdesk_bios)

今回は、

1. Update AMD AM4 AGESA V2 PI 1.2.0.3 Patch A

2. Improve system stability

の更新です。

ベータBIOSの3801よりもマルチコアでの性能が改善されています。

PBO2のAutoで最適が進んですべてAutoにすると最速のスコアがでます。

PBO2でのこれまでの最適値とされていた電圧カーブとコア電圧をオフセットで下げる設定をしているとシステムごと落ちます。

マニュアルでOCして4.75GHzだとCINEBENCH R20が落ちるので、4.725GHz固定でベンチマークを取ってみます。

4.725GHzまでなら、OCが影響していると思われるメモリやキャッシュ周りのエラーWHEA ID:18が出ることがないようです。

4.725GHzでのベンチマークスコア

CINEBENCH R20

マルチ　：6815

シングル： 608

[![](/img/o1646079014961135854.png)](/img/o1646079014961135854.png)

CPU-Z

マルチ　：6842

シングル： 654

[![](/img/o0417041914961135889.png)](/img/o0417041914961135889.png)

すべてAutoで設定するとシステム全体の安定性が向上しているので、BIOS更新のリスクを許容できる人は更新をお勧めします。
