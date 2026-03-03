---
title: "SMR方式のHDDでROBOCOPYを使う場合のパラメーター"
date: 2021-03-24T09:47:05+09:00
archives: ["2021-03"]
original_url: https://ameblo.jp/yuki9902/entry-12664243762.html
categories: ['COMPUTER']
---

Windowsの堅牢性の高いファイルコピー機能「ROBOCOPY」ですが、コピー先がSeagate社製のSMRのHDDだと、そのままでは非常に書き込みが遅くなります。

5MB/s程度になります。

これを回避するには、ROBOCOPYのパラメーター[/B][/Z]を使わないようにし、[/J][/NOOFFLOAD][/MT:1]を使うようにします。

重要なのは、SMRのHDDに対してです。

現行のWindows10のI/O制御、キャッシュ機能とSeagate社製SMR HDDの内部キャッシュ制御方式とは相性が悪いです。

ROBOCOPYのパラメーターを適切に設定すれば、100MB/sから80MB/s程度で書き込めます。

SMR HDDで苦労している人は見直してみてください。

買うならCMR方式のHDD

[![](https://p.odsyms15.com/rpBMFRnHZSIVVDE86pJAB1)

TOSHIBA 東芝 3.5" 内蔵HDD 8TB(CMR) 7,200rpm SATA 24x7 RVセンサー搭載 NASに最適ハードディスク 国内正規品 3年保証 国内サポート対応 故障時の同時交換対応 MN06ACA800/JP

Amazon（アマゾン）

18,384〜38,000円](https://d.odsyms15.com/click?aid=flhR3m56HmKtBDQcIHOgc5&mimp=oBTGwud8pJzseTzIT6BPZh&session=b5eedc55-d526-4852-874c-0e63dbb54d97&uid.p=d0c67ab0-a27d-4b12-a318-ce4fc1365a64&ext.referrer=blank)

苦労したいマゾな人はSMR方式のHDD

[![](https://p.odsyms15.com/Y9C3UKPmH3R4HKn6ME4L87)

Seagate BarraCuda 3.5" 8TB 内蔵ハードディスク HDD 2年保証 6Gb/s 256MB 5400rpm 正規代理店品 ST8000DM004

Amazon（アマゾン）

13,404〜24,800円](https://d.odsyms15.com/click?aid=b298RmQP9H4LW0werOTaO2&mimp=NC12HHVkJR2KdO8wJcDhGw&session=b5eedc55-d526-4852-874c-0e63dbb54d97&uid.p=d0c67ab0-a27d-4b12-a318-ce4fc1365a64&ext.referrer=blank)