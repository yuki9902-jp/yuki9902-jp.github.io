---
title: "Corsair iCUE LINK TITAN 240 RX RGB"
date: 2025-01-28T12:17:46+09:00
archives: ["2025-01"]
original_url: https://ameblo.jp/yuki9902/entry-12884168194.html
categories: ['COMPUTER']
---

水冷ヘッドを壊してしまった。

Corsair [iCUE H115i ELITE CAPELLIX XT](https://www.corsair.com/jp/ja/p/cpu-coolers/cw-9060069-ww/icue-h115i-elite-capellix-xt-liquid-cpu-cooler)（280mmAIOクーラー黒）と[iCUE ELITECPU クーラー LCDディスプレイアップグレードキット](https://www.corsair.com/jp/ja/p/cpu-coolers/cw-9060056-ww/icue-elite-cpu-cooler-lcd-display-upgrade-kit-cw-9060056-ww)をセットにして使用していましたが、クーラーのヘッド部分が熱くなってくるとLCDの下半分の表示が乱れてしまう問題があり、イライラしてました。

先日、また表示が乱れたので、何度か再起動したりしても直らず、イライラしたので電源が入ったままLCDキットを本体から抜いて差し直したら、クーラーのヘッド部分のファームウェアが壊れてしまいました。

iCUE制御ソフトウェアからヘッド部分が認識できなくなり、ポンプの制御が出来なくなり一定速度でしか回転しなくなり、LCDの表示が出来なくなり、LEDも消灯してしまいました。

さすがにCPUの冷却するための物で壊れたままは不味いので、パソコン工房の通販で新しくCorsair [iCUE LINK TITAN 240 RX RGB AIO 水冷式CPUクーラー](https://www.corsair.com/jp/ja/p/cpu-coolers/CW-9061016-WW/icue-link-titan-240-rx-rgb-aio-liquid-cpu-cooler-cw-9061016-ww)黒を買いました。

CorsairのiCUE LINKという新しい接続方式になりファンやクーラーヘッダへの接続が少ないケーブルで済むのでケース内がすっきりします。

[![](/img/o2014151115537984959.jpg)](/img/o2014151115537984959.jpg)

ただ、PCI-Eの8pin(6+2pin)電源ケーブルが1本必要になるので、安物の電源ユニットでは採用が難しいです。

冷却能力は280mmから240mmにグレードダウンしましたが、先のAIOは経年で冷却液が少なくなっていたこと、クーラーとファンの制御の見直しもありよく冷えています。

CPUは、AMD RYZEN 9 5900XTで、これをPBOでカーブオプティマイズしてやると190W近くまで消費してCinebench R23で30000ぐらいの値になりました。

ノーマルで使うより10％前後高速になっています。

急な出費になってしまいましたが、性能的には概ね満足な物でした。