---
title: "Windows10 Pro 64bitでファイルサーバーのメンテナンス"
date: 2021-04-18T14:55:10+09:00
archives: ["2021-04"]
original_url: https://ameblo.jp/yuki9902/entry-12669275903.html
categories: ['COMPUTER']
---

[![](https://stat.ameba.jp/user_images/20210418/14/yuki9902/b0/e6/j/o4000300014928239889.jpg?caw=800)](https://ameblo.jp/yuki9902/image-12669275903-14928239889.html)

5400rpmの3.5インチHDD 4台を5.25インチベイに設置するために、ホットスワップに対応した簡単着脱が出来る変換ベイを買いました。簡易ロックを解錠して、ノブを引き扉を開くとHDDが外に出てきます。

それからSATAケーブル、増設したSATA電源ケーブルが赤色なので、PC内部のLEDも赤色に設定しました。

[![](https://stat.ameba.jp/user_images/20210418/14/yuki9902/4d/e0/j/o4000300014928239892.jpg?caw=800)](https://ameblo.jp/yuki9902/image-12669275903-14928239892.html)

吸気が2つ、排気が1つでPC内部が正圧でエアフローが少なかったので、かなり古い12センチファンがあったのでCPUの上、ケースの上面に設置し、エアフローの改善を図りました。PC内部が負圧で、増設したHDDベイの吸気口からもエアを吸います。

Windowsのダイナミックボリュームでミラーボリュームを構成していましたが、7200rpm3TB(CMR)×4台、5400rpm3TB(CMR)×2台、5400rpm8TB(SMR)×2台を括りにして、もう一度Windows10の記憶域（シンプロビジョニング）を使って構成し直しました。

ホットスワップ対応の増設ベイに5400rpm8TB(SMR)を入れました。将来的にCMRのHDDに置き換えるつもりです。