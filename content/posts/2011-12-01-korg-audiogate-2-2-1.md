---
title: "KORG AudioGate 2.2.1"
date: 2011-12-01T23:41:13+09:00
archives: ["2011-12"]
draft: false
categories: ['AUDIO']

---

KORG AudioGate が2.2.1にバージョンアップして、Windows7/VISTAにおけるWASAPI共有モードに対応しました。

WASAPI共有モードなので、ビットパーフェクトは保証されませんが、WASAPI共有モード自体は32bit Floatで処理しているそうなので、24bit IntegerのWAVEデータなら問題はないでしょう。

32bit IntegerのWAVEファイルは存在してたり、作成することはできるのですが、私の持っているONKYO SE-200PCI LTDは、192kHz/24bit(Integer)までのフォーマットにしか対応していませんので、必要ないです。

それにPCMの32bit Integerより、DSDデータをダイレクトでアナログに変換するD/Aコンバーターを手に入れる方がよっぽど現実的でしょう。いやDSDの方がマイナーなのか。

ただ32bit Integerの分解能を生かせるデータは、DSDからの変換しか存在しないでしょうから、だったらDSDのままが良いんじゃないのかな。

ただ世の中に32bit Integerを必要とする音楽ソースがないのも事実だけどね。

むしろ高音域にのってくる量子化ノイズ、ビートダウンノイズ対策が大変になってくる分、音質上メリットが少ないかも。