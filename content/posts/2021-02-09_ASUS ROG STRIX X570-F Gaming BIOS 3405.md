---
title: "ASUS ROG STRIX X570-F Gaming BIOS 3405"
date: 2021-02-09T21:05:42+09:00
archives: ["2021-02"]
original_url: https://ameblo.jp/yuki9902/entry-12655675244.html
categories: ['COMPUTER']
---

[ASUS ROG STRIX X570-F Gaming のBIOS 3405](https://rog.asus.com/jp/motherboards/rog-strix/rog-strix-x570-f-gaming-model/helpdesk_download) が公開されました。

1. Update AMD AM4 AGESA V2 PI 1.2.0.0

2. Update AMD RAID UEFI driver

3. Improve system stability

PBO2のカーブの仕様が変更になったようです。

PBO2でチューニングしても、Cinebench R20のスコアが3402 Betaより5％ほど下がります。

FF14漆黒のヴィランズのスコアは1％ほど下がります。

SoC電圧の設定できる幅が狭くなっていて、電圧を下げて高クロックを狙うと突然落ちます。

PBO2をAutoで使っても速くはないので、設定が難しいです。

とりあえず、高性能コア -5、他のコア -30、コア電圧 マイナスオフセット、0.05V。

水冷で全コアOCした方が良いかも。