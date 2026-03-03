---
title: "Windows10 Pro 64bitでファイルサーバーの構築 その後"
date: 2021-04-05T11:53:55+09:00
archives: ["2021-04"]
original_url: https://ameblo.jp/yuki9902/entry-12666718592.html
categories: ['COMPUTER']
---

HDDを２台ずつで双方向ミラーをしたのでは、Windowsのダイナミックディスクによるミラー構成より遙かに速度が遅いので、記憶域を削除して、すべてのHDDをダイナミックディスクによるミラーリングに変更しました。

それに伴い、HDDの速度はシーケンシャルリードで300MB/s、シーケンシャルライトで180MB/sになりました。

これでは2GbpsのEthernetの速度では間に合わないので、ファイルサーバーに1Gbpsのネットワークインターフェイスを追加しました。

SMBなら３ポートでバランシングして送受信できます。

ネットワークインターフェイスはLANケーブルと一緒にポイントなどを使って1,000円ほどで買ったのでかなりやすく上がりました。

2.5Gbpsのスイッチがやすくなったら導入を検討します。

バックアップの速度向上のためだけでは、10Gbpsはまだ高すぎます。

[![](https://p.odsyms15.com/6dLgbITqkSmPxcH3yjhrU1)

TP-Link 1000BASE-T/100BASE-TX/10BASE-T対応PCI-E バス用ギガビットLANアダプター TG-3468

Amazon（アマゾン）

1,100〜2,191円](https://d.odsyms15.com/click?aid=bjmAKlKcyXWpB7Net4JMc5&mimp=kn4qqKi7jxOgy27tSsCPg9&session=7e4f2cdf-01aa-4931-ba17-3e15aa612ef4&uid.p=d0c67ab0-a27d-4b12-a318-ce4fc1365a64&ext.referrer=blank)

[![](https://p.odsyms15.com/bbB6Ko0hYVMCV1LPXxdRX6)

OKN 2.5G BASE-T PCIEネットワークアダプタ2500/1000/100Mbps PCI Express Gigabit Ethernet LANカード RJ45 LANコントローラ Windows Server/Windows/Linux対応、標準および低プロファイラーブラケット

Amazon（アマゾン）

3,680円](https://d.odsyms15.com/click?aid=sXQ30ZBCcdpW5wikZW5u37&mimp=TXKHVpqCP2qQxBlCrSDnWi&session=7e4f2cdf-01aa-4931-ba17-3e15aa612ef4&uid.p=d0c67ab0-a27d-4b12-a318-ce4fc1365a64&ext.referrer=blank)

[![](https://p.odsyms15.com/h7YybT5rKF6o7u689rFKK5)

エレコム LANケーブル CAT6A 3m 爪折れ防止コネクタ ブラック LD-GPA/BK3

Amazon（アマゾン）

462〜1,640円](https://d.odsyms15.com/click?aid=gOZIKNUM0seW59J9mkcL16&mimp=IbMpAlMck50GsH1wKI8zUJ&session=7e4f2cdf-01aa-4931-ba17-3e15aa612ef4&uid.p=d0c67ab0-a27d-4b12-a318-ce4fc1365a64&ext.referrer=blank)