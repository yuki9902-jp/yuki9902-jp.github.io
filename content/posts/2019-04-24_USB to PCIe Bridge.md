---
title: "USB to PCIe Bridge"
date: 2019-04-24T23:54:27+09:00
archives: ["2019-04"]
original_url: https://ameblo.jp/yuki9902/entry-12456646568.html
categories: ['COMPUTER']
---

先日、交換したNVMeのSSDのお古を活用するため、USB3.1 Gen.2対応のM.2 NVMe SSDケースを買いました。

性能はかなり高いと評判ですが、価格も高めでした。

[M.2 NVMe SSD to USB3.1 Gen.2 アルミケース 防塵耐水モデル (CAM2NVU31CBP)](http://www.century.co.jp/products/cam2nvu31cbp.html)

防塵、耐水機能もあって、衝撃吸収バンパーも付いてます。

星形ネジなので、専用ドライバーも付いてきます。

SSDと変換基板の間には隙間があるので、そこに後から1ミリ厚の熱伝導シートを挟み込みました。

第1世代のWD BLACK 512GBを使って、シーケンシャルアクセスで850MB/s程度、ランダムアクセスで90MB/s程度です。

USB3.1Gen.2の理論値が1012MB/sなので、NVMeからUSBへの変換などのオーバーヘッドを考えてもなかなか良い数値が出ているように思います。

あと、Crystal Disk Mark 6.0.2を走らせると書き込み速度を測定中にフリーズします。

この場合、Windowsも無応答になりますが、USBケーブルを抜けば、復帰します。

これはCrystal Disk Mark側の不具合だと思います。

さて、PCに内蔵しているSATAのSSDより速いですが、今のところ使いどころが思いつきません。

キャッシュディスクとして使うために、PCIeバスに差し込むM.2変換ボードの方が良かったかなぁ。