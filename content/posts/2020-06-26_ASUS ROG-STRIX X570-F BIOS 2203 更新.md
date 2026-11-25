---
title: "ASUS ROG-STRIX X570-F BIOS 2203 更新"
date: 2020-06-26T01:25:20+09:00
archives: ["2020-06"]
original_url: https://ameblo.jp/yuki9902/entry-12606876667.html
categories: ['COMPUTER']
---

ASUSのダウンロードページには、AMD AGESA AM4 PI 1.0.0.1の更新としか説明に書かれていないので詳細はよく分かりません。

マイクロコードのバージョンが上がっているのでまあ何か変わったんでしょう。

マイクロコードのバージョンから推測するに、AM4 combo V2 PI 1.0.0.1 patch Bのことだと思います。

ドイツ語の情報で、このマイクロコードでは、500系、400系、300系チップセットで、RYZEN 3000XTシリーズと今後リリース予定のRenoir APUへの対応、ZEN3コアは、400シリーズ以降で対応と出ています。

BIOS 2203では、メモリーの安定性が改善されているらしいですが、G.SKILLのTrident Z NEOのS.K.HynixのCダイで、XMP2（ASUSだとD.O.C.P）の読み込みがうまくいかない例が英語のサイトでいくつか挙がってます。

私が持っているG.SKILL Trident Z NEO 3600MHz CL18では、CPU-Zの値を見るとSamsung Bダイが使われているようですし、動作にも特に問題は出てないです。

ASUSが公開しているメモリー対応表では、G.SKILL Trident Z NEO 3600MHz CL18はS.K.HynixのCダイが使われていることになっていますが、出荷時期にや地域によって使用しているチップが違うんでしょうか、よく分かりません。

RYZEN 3000XTシリーズを持っていなければ、BIOS 2203にしても目に見えて何か変わるわけではないので、更新は慎重にしましょう。