---
title: "ASUS ROG STRIX X570-F GAMING BIOS 3402 Beta"
date: 2021-01-17T20:34:16+09:00
archives: ["2021-01"]
original_url: https://ameblo.jp/yuki9902/entry-12650890924.html
categories: ['COMPUTER']
---

ASUS ROG STRIX X570-F GAMINGのBIOS 3402 Betaが公開されたので適用しました。

AM4 AGESA V2 PI 1.2.0.0のアップデートです。

更新内容はまだ分かっていません。

今後発売されるNVIDIA GeForce RTX 3060Ti 12GBで、AMD SAM(Re-size BAR)が使えるようになり、それ以外のRTX 30シリーズはNVIDIA側でvBIOS更新で対応するようです。

PBO2の性能は相変わらずで、全く使いどころがないです。

なんでコア電圧があんなに上がるんでしょうね。

手動オーバークロックとコア電圧自動の方が、最大負荷時に電圧が低いのはなぜなんでしょうかね。

追記：

ClockTuner for Ryzenの開発を手がける[Yuri Bubly](https://twitter.com/1usmus)によると

「I see interesting information that AGESA 1.2.0.0 contains only "bug fixes". It does not. SMU 56.44.00 contains a number of improvements to the Curve + improvements for the dLDO injector. Also AGESA 1.2.0.0 has no problems with WHEA on FCLK 1900.

(This only applies to Zen 3)」

ということで、PBO2の曲線の改善と電圧レギュレーターdLDOインジェクター（デジタルLow Drop-Out)の改善が含まれているそうです。

実際、PBO2で設定した場合のCINEBENCH R20のマルチコアの値が少しだけ改善しました。

最大4.625GHz(160W、85℃)で5600前後ですけど。

Betaなので、特別にRAMのOCしたい場合じゃなきゃ、更新は見送るべきです。