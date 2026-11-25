---
title: "SMB Direct"
date: 2020-12-30T13:47:40+09:00
archives: ["2020-12"]
original_url: https://ameblo.jp/yuki9902/entry-12647067899.html
categories: ['COMPUTER']
---

Windows 10 Proには、CPUへの負荷を極力減らしネットワークインターフェイスが直接メモリにアクセス出来る機能「SMB Direct」が追加されています。

これを有効にすることでネットワークのパフォーマンスが改善されます。

有効にするためにはWindows PowerShellで、

```
Set-NetOffloadGlobalSetting -NetworkDirect Enabled
```

と入力して、クライアント側、サーバー側の両方で設定します。

ネットワークブリッジを有効にしていると、この機能が無効になります。

昨日はネットワークブリッジを有効にして、帯域を2Gbpsに拡大させましたが、速度は遅くなっていました。

今日、ネットワークブリッジを解除し、ジャンボフレームを9KB MTUに設定して、SMB Directの無効と有効で速度計測を行いました。

CrystalDiskmarkのシーケンシャルリードで90MB/s(750Mbps)から120MB/s(1GBps)に上がりました。

シーケンシャルライトでは80MB/sから90MB/sに上がりました。

ランダムライト、ランダムリードともに変わりません。

ランダム性能はHDDがボトルネックになっているのでSMB Directに影響されることはありません。