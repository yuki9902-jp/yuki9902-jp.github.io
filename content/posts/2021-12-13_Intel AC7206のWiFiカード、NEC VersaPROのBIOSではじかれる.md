---
title: "Intel AC7206のWiFiカード、NEC VersaPROのBIOSではじかれる"
date: 2021-12-13T17:59:14+09:00
archives: ["2021-12"]
original_url: https://ameblo.jp/yuki9902/entry-12715480322.html
categories: ['COMPUTER']
---

IEE802.11 ac/g/nのIntel AC7206デュアルバンドWiFi&Bluetooth4.0アダプターカードをNECのVersaProのWiFiカードと置き換えようと買ったんですが、BIOSではじかれて起動できません。

どうやら規制対象の某国製のPCに搭載されたWiFiカードはSIDが厳格に管理されていて、BIOSのリスト内に存在しないカードを搭載した場合は起動しないようにされているようです。

NECの販売ですが、中身は某国のLenovo製なので、仕方ないと言えば仕方ないのかな。

BIOSを改造すれば起動できるようになるそうですが・・・。

IEE802.11acの速度は諦めるしかないか・・・。