---
title: "Raspberry Pi 4でActive Directoryを（失敗）"
date: 2021-01-12T22:22:55+09:00
archives: ["2021-01"]
original_url: https://ameblo.jp/yuki9902/entry-12649885829.html
categories: ['COMPUTER']
---

LAN内にメインPC、ファイルサーバー、ノートPC（ラップトップw）があり、自分のユーザーアカウントの管理を一元化したほうが良いのか、STANDALONEで管理した方が良いのか迷い中。

そして手元には正直使い道に困っているRaspberry Pi 4Bの4GBモデルがあります。

64bit OSが動く環境でもありますが、Ubuntu 20.1 64bit Desktopの公式版をインストールしてみました。

Desktop版はRaspberry Pi 4B 4GBでは重いです。

ディスクがSDカードなのでしょうがないですね。

で、次にRaspberry Pi OSをインストールして、Active Directoryの構築を試みました。

DNSをSAMBAに内蔵されたDNSサーバーを使うように設定していきましたが、Port 135の通信が出来ずにDNSの逆引き登録が出来ません。

Portの開き方が分からず、FirewallをインストールしてPortを開ける方法を試そうとしましたが、Firewallのインストールに失敗します。

Raspberry Pi 3でActive Directoryの構築をしているサイトを参考にしていましたが、簡単にはいきません。

RaspiOSでの構築は一旦諦めます。

今は、Ubuntu 20.1 Server 64bitをSDカードに書き込みました。

今日はもう面倒なので構築はまた明日にします。