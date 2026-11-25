---
title: "Install Windows11  with AMD RYZEN 7 1700 & X370"
date: 2023-07-12T21:53:42+09:00
archives: ["2023-07"]
original_url: https://ameblo.jp/yuki9902/entry-12811827940.html
categories: ['COMPUTER']
tags: ['AMD','RYZEN','X370','BIOS','1700','GIGABYTE','Windows11Pro']
---

Windows11 がリリースされた当初、RYZENの初代はサポートされていませんでした。

X370マザーボードは、GIGABYTEのGA-AX370-Gaming K7 (rev.1.0)を使っていますが、最新のBIOS[F51i]が2023年2月10日付けで公開されていたので、更新しました。

BIOS項目の中でTPM2が追加されていて、Windows11の要件を満たしました。

TPM2を有効にして、Windows11 Proをクリーンインストールしました。

特にエラーも出なく、問題なくインストールが完了しました。

マザーボードのドライバーは、Realtek HD Audio Driverぐらいで、あとはAMDのサイトからチップセットドライバーとGPUのドライバーをインストールするだけです。

ちょっとトラブルがあって、NASのHDDに貯めていた諸々のデータを削除したので、TrueNASをインストールしていたRYZEN 7 1700マシンですが、Windows11 Proにしました。

RYZEN 7 5800XのメインPC側もデータを削除して、1TBのSATA SSDが4台余ったので、これをRYZEN 7 1700マシンに接続して、4TBのRAID0（ストライピング）にしたら連続読み書き2000MB/sぐらいになったので、NVMe並の使い勝手になりました。

引き続きデータ保存用に使うのと、それとnViDIA GeForce GTX 1050 TI 4GBを搭載しているので、AI画像生成とかゲーム動画配信とかにしてみても良いかなと思います。

RADEONだと動かないAI画像処理関係が、さほど問題なく動くのでいろいろ出来そうです。

RTX3060 12GBがどこかで安く売ってないかな。