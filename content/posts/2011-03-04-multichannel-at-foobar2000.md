---
title: "Multichannel at Foobar2000"
date: 2011-03-04T16:47:57+09:00
archives: ["2011-03"]
draft: false
categories: ['AUDIO']

---

2ch Stereoの楽曲を、NERO WaveEditorで7.1chと5.1chに変換してみました。

7.1ch Wave Format (44.1khz/16bit)と5.1ch Wave Format(192kHz/24bit)です。

Foobar2000はSoXResamplerとWASAPIのcomponentをinstallしてあります。

7.1chはWASAPI componentを通しての再生は出来ませんでした。Formatが未対応ということで、8ch再生には対応できません。

WASAPIをbypassすると再生出来ます。

つぎに5.1chです。こちらはWASAPI componentを通して再生出来ます。ということでWASAPI componentは6chまで対応していることが分かりました。

SoXResamplerは8chでのup convertも可能です。ただしかなりCPUの能力がないと処理落ちすることでしょう。

それから6ch 192kHz 24bitのWave Format Fileは毎秒27MBの転送レートが必要です。5分ぐらいの曲なら1ファイル当たりのサイズも1GBになります。Wave形式は2GBまでですのでup convert fileをつくるなら注意が必要です。