---
title: "Cooler Master MasterAir MA620MとAMD RYZEN 7 5800X"
date: 2020-11-29T01:19:01+09:00
archives: ["2020-11"]
original_url: https://ameblo.jp/yuki9902/entry-12640861560.html
categories: ['COMPUTER']
---

[『Cooler Master MasterAir MA620M』 Cooler Master MasterAir MA620M CPUクーラー MAM-D6PN-120PA-R1 FN1352Amazon（アマゾン）11,…!ameblo.jp![](https://stat.ameba.jp/user_images/20200404/00/yuki9902/36/40/j/o0966064014738248035.jpg?caw=800)](https://ameblo.jp/yuki9902/entry-12592101951.html)

全コア4.7GHzまでオーバークロックしたRYZEN 7 5800Xを、CPU-Zで全コアに100%のストレス（負荷）をかけて、CPUクーラーCooler Master MasterAir MA620Mでどれだけ冷やせるか確認してみました。

[![](/img/o1014052314858587517.png)](/img/o1014052314858587517.png)

ファンの回転制御はASUSのAI Suite 3のFan Xpert 4で行います。

[![](/img/o0417041914858588964.png)](/img/o0417041914858588964.png)

6670から6700前後で推移しますが、大きくはぶれません。

[![](/img/o0636079314858589076.png)](/img/o0636079314858589076.png)

CPUの消費電力は127Wから129Wで推移します。

クロックは4699MHzで安定しており、CPU16スレッドのうち1～2つぐらいのスレッドの使用率がたまにぶれますが、概ね安定しています。

CPUパッケージの温度は77度ぐらい、CPUコアの温度は65度ぐらいで、CPUファンは1300rpm前後で安定しています。

130W近い消費電力ですが、発熱量は意外に少ないのかな。

MA620Mのファンは最大2000rpmなので、1300rpmで65度を維持して4.7GHzからクロックが落ちたりはしないので、しっかりと排熱できているようです。

ただ、現在の室温が16度ということを考えると、ヘッドルームは20度ぐらい余裕がないと夏場はかなりキツいと思います。

AMD RYZEN MASTERでPrecision Boost Overdriveを有効にして負荷テストをすると、クロックが4.525GHzで、AMD RYZEN MASTERの表示値で90度に達するので、いまいち何が正しいCPU温度か分かりません。

AMD RYZEN MASTERで4.7GHzにOC設定するとPCが即落ちるので、AMD RYZEN MASTERはアンインストールしました。

ASUSのAI suite 3の方が簡単に設定できるので、AGESAの新しいBIOSが配布されるまでは、こちらで行きます。
