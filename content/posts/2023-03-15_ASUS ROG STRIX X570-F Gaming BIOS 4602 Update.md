---
title: "ASUS ROG STRIX X570-F Gaming BIOS 4602 Update"
date: 2023-03-15T23:20:43+09:00
archives: ["2023-03"]
original_url: https://ameblo.jp/yuki9902/entry-12793894263.html
categories: ['COMPUTER']
tags: ['AMD','AGESA','ASUS']
---

[ASUS ROG STRIX X570-F GamingのBIOS バージョン4602](https://rog.asus.com/jp/motherboards/rog-strix/rog-strix-x570-f-gaming-model/helpdesk_bios/)がリリースされました。

更新内容は、AGESA ComboAM4v2PI 1208が適用されました。

今回のAGESAの内容は、AMD RYZENシリーズ、Athlonシリーズ、AMD RADEON RXシリーズのプロセッサにおけるセキュリティーの脆弱性の緩和です。

[AMD Graphics Driver Vulnerabilities – November 2022](https://www.amd.com/en/corporate/product-security/bulletin/amd-sb-1029)

リンク先のタイトルでGPUドライバーのセキュリティー問題だと思われやすいですが、ページの中程に、Desktop向けのCPU、APUの中にGPUを搭載していないCPUも対象となっていることが書かれています。

2022年11月にCVE-2020-12930など一連の問題が、Radeon RXプロセッサの脆弱性で報告されていますが、CPUも同様の問題を抱えていたようです。

脆弱性の深刻度がHighとMediumが改善されているので、BIOS バージョン4602に更新した方が良いでしょう。

今回のアップデートでCPUのパフォーマンスにはほぼ影響していないように見えます。

極一部のゲームでfpsが向上しているものもあるようですが、パフォーマンスの改善は今回のアップデートでは言及されていません。

またAMDのサイトからチップセットドライバーもダウンロードして更新した方が良いです。

いくつかのバグフィックスがされていて、USB周りも安定性が向上すると思われます。