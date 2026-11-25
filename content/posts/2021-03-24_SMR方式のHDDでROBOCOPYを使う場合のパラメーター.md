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
