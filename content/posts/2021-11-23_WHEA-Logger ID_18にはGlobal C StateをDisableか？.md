---
title: "WHEA-Logger ID:18にはGlobal C StateをDisableか？"
date: 2021-11-23T15:01:23+09:00
archives: ["2021-11"]
original_url: https://ameblo.jp/yuki9902/entry-12711846899.html
categories: ['COMPUTER']
---

[『解決方法：致命的なエラー WHEA-Logger ID:18でWindowsが落ちる』１．解決方法（１）BIOS（UEFI）の設定をすべて出荷時デフォルトに戻す。（２）低電力設定をやめる。　・Global C StateをDisableにする。…![リンク](https://c.stat100.ameba.jp/ameblo/symbols/v3.20.0/svg/gray/editor_link.svg)ameblo.jp![](https://stat.profile.ameba.jp/profile_images/44/yuki9902/1246028974083.jpg)](https://ameblo.jp/yuki9902/entry-12957494856.html)

　Ryzen 7 5800XのメインPCにWindows11をインストールしてから、WHEA-Logger ID:18が頻発しています。

　PCの電源を入れたまま放置していると、いつの間にか再起動しています。

　オーバークロックだろうとオートだろうとCPUがアイドル時から突発的な負荷が掛かると落ちているように見えます。

　ということで、CPUの省電力制御を有効にしているGlobal C StateをDisableにしてみました。

　PBO2の電圧カーブで、優秀なコア-5、他のコア-20に設定して、OCCTのデータセット大で5分間、Cinebench R23の10分間の負荷テストはクリアしました。

 室温20度で、CPUパッケージの温度はアイドル時40度、OCCT負荷時70度、CinebenchR23負荷時78度で安定しています。ちなみに280ミリの簡易水冷です。

　しばらくこれで運用してみて、安定するか確かめてみます。

　ちなみにLinuxやBSDでは、Ryzen全シリーズでGlobal C StateをDisableにしないと不安定になるようで、この設定は必須です。