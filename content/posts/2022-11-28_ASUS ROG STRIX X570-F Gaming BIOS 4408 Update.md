---
title: "ASUS ROG STRIX X570-F Gaming BIOS 4408 Update"
date: 2022-11-28T10:18:35+09:00
archives: ["2022-11"]
original_url: https://ameblo.jp/yuki9902/entry-12776700469.html
categories: ['COMPUTER']
---

AMD RYZEN ZEN3用のAMD X570チップセットを搭載したマザーボード、ASUS ROG STRIX X570-F GamingのBIOS 4408が、2022/11/25付けで公開されたので、早速適用しました。

変更内容は、システムの互換性の向上です。

適用後、DDR4メモリのXMP2に相当するD.O.C.Pを設定し、なぜか読み込めないtPRの値を手動で84から64に変更します。

再起動後、さらにPCI-Eの4GBデコードを有効、ReSizeBARを有効、警告が表示される方のCPU OCの項目の中でPBO2をAdvancedにして、TDPの制限をMotherBoardに設定、動作周波数の変更をPositiveにして、変更幅を200に設定、他にSoC/UncoreのOCは無効にします。（SoCはOC耐性がほぼないので、ここを有効にしてOCすると落ちる可能性が非常に高くなります。）

電源供給の設定を130%でExtreamに設定、ロードラインキャリブレーションはAutoにします。パワーマネジメントのS3項目が消えていたので気にせず再起動。

搭載しているCPUはRYZEN 7 5800Xで、280ミリの簡易水冷で、メモリは3600MHz CL18の32MBです。

今は限界を攻めたOC設定はしていないので、少ないスレッドなら5050MHz、全負荷で4700MHzの最大130Wで動作します。

OCCTの負荷テストで、CPUパッケージの温度は74度ぐらいで安定します。

実用環境にしているので常駐ソフト等が動いているので、CPUベンチマークを採るには向いていませんが、RYZEN 7 5800Xの指標値には近い値が出ています。