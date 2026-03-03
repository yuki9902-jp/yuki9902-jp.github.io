---
title: "ASUS ROG STRIX X570-F Gaming BIOS 3001 Update"
date: 2020-12-09T17:57:18+09:00
archives: ["2020-12"]
original_url: https://ameblo.jp/yuki9902/entry-12643016924.html
categories: ['COMPUTER']
---

「[ASUS ROG STRIX X570-F GamingのBIOS バージョン3001](https://rog.asus.com/jp/motherboards/rog-strix/rog-strix-x570-f-gaming-model/helpdesk_download/)」が公開されました。

新しいCPUのサポートとAMD SAM(Smart Access Memory)を使用できるようにするための「ReSize BAR」の項目が追加されました。

他にPrecision Boost Overdrive 2に関連する項目が表示されていたのでAGESA 1.1.8.0が適用されたBIOSだと思います。

PBO2の項目の設定方法がいまいち分からないですが、使っていないコアの電圧を引き下げて電力と熱容量を確保し、負荷の高いコアに余った電力を供給して性能向上を図るらしいです。

AMDのスライドを使っただけの概要はAMD HEROSに紹介されていますが、個体によって設定値が異なるので、自分で追い込んでいく必要があるみたいです。

設定してみましたが、sweet spotを外しているみたいで大幅に性能ダウンしてしまうので、追い込みは難しいです。

面倒くさいので、全コア4.725GHzにオーバークロックにしました。

PBO2に関しては、日本語で詳しく設定方法を解説した情報がでるまで待ちます。

PBOも使わなかったし、結局PBO2も使わないような気がします。

AMD SAMついでにPCI-Eの設定項目の中に「Above 4G Decoding」があります。

32bitの限界を超え4GBを超えるデータを一気に読み書きできます。

64bit OSを使っている場合はONにしておけば、もしかしたら良いパフォーマンスを得られるかもしれません。