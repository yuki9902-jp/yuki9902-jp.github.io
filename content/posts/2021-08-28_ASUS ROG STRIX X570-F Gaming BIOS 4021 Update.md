---
title: "ASUS ROG STRIX X570-F Gaming BIOS 4021 Update"
date: 2021-08-28T01:38:09+09:00
archives: ["2021-08"]
original_url: https://ameblo.jp/yuki9902/entry-12694629041.html
categories: ['COMPUTER']
---

ASUS ROG STRIX X570-F GamingのBIOS 4021が公開されました。

[ROG Strix X570-F Gaming | ROG Strix | Gaming マザーボード｜ROG - Republic of Gamers｜ROG 日本PCIe 4.0、Aura Sync RGBライティング、Intel Gigabitイーサネット、ヒートシンク付きデュアルM.2、SATA 6Gbps、およびUSB 3.2 Gen 2を搭載したAMD X570 ATXゲーミングマザーボード![リンク](https://c.stat100.ameba.jp/ameblo/symbols/v3.20.0/svg/gray/editor_link.svg)rog.asus.com](https://rog.asus.com/jp/motherboards/rog-strix/rog-strix-x570-f-gaming-model/helpdesk_bios)

更新内容は、AMD AGESA V2 PI 1.2.0.3 Patch Cとシステムのパフォーマンスの改善です。

AGESA V2 PI 1.2.0.3 Patch Cでは、APU RYZEN 5000Gシリーズの対応、CPU RYZEN 5000シリーズのサポートの拡張、RYZEN 5000シリーズで発生していたすべてのUSBの問題の解決が主なようです。

実際に導入してみたところ、RYZEN 5000シリーズの機能が拡張されていてUEFIの項目が結構変更されています。

細かいところまで把握できていませんが、D.O.C.P.、PBO2、PCIEの転送幅の拡張の有効化、Resize BARの有効化、データリンクエクスチェンジの有効化を行って、後はほぼ初期値で起動させました。

BIOS 4021でCPU-Zでしかベンチマークを取っていませんが、BIOS 4010 Betaとほぼ変わりはないようです。

0.5%程度の揺らぎなので正確な違いは分かりません。

USBに問題がある場合には更新しましょう。

それから、AMDのサイトでチップセットドライバーも更新されていたので適用しました。

RYZENに対応している情報がない型番のCorsairのVENGENCE PRO RGB 3600MHzCL18を購入してしまい、ずっとRGB LEDの動作に若干問題がありましたが、チップセットドライバーを更新したら問題がなくなりました。

チップセットドライバーの更新内容を見ましたが、関係ないはずなんですが。

ただし致命的なセキュリティーに関する更新なので必ず更新しましょう。