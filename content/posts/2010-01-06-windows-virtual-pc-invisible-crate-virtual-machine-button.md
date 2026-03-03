---
title: "Windows Virtual PC - Invisible Crate virtual machine button -"
date: 2010-01-06T12:34:03+09:00
archives: ["2010-01"]
draft: false
categories: ['COMPUTER']
tags: []
---

Windows 7 のWindows XP Mode を利用するだけでなく、Windows Virtual PC から他のゲストOSをインストールできるらしい。Linux をインストールしたくて、チャレンジしてみたが、不具合があり、断念している。この不具合で仮想マシンを作成できず、他のOSをインストールできないからだ。

不具合は、 Windows Virtual PC の 「仮想マシン」フォルダを開いたときにメニューバーに「仮想マシンの作成」ボタンが表示されないことだ。どこのサイトを見ても、このボタンが表示されていることで、説明されている。このボタンがないと、どこからも仮想マシンを作成することが出来ない。

さて非常に困った。Windows XPでなければならない理由はないが、Windows Me と Linux は必要なのでインストールしたい。Windows 7 にアップグレードする際に、Windows VISTA  Ultimate x64 から上書きインストールしたのが原因だろうか。

他のサイトでこの問題に遭遇した記事があり、フォルダのセキュリティーを”読み取り専用”のチェックをはずすということで解決できたとある。しかし、この方法では解決できなかった。もう一つこの問題に遭遇した記事を見つけたが、私と同じく解決できずにあきらめたらしい。

この際、HDDの整理を兼ねて、Windows 7 Ultimate 64bit をクリーンインストールしてみようと思う。

～追記～

[http://social.technet.microsoft.com/Forums/en/w7itprovirt/thread/24ae635f-41a7-4c50-bcae-81cba3112b32](http://social.technet.microsoft.com/Forums/en/w7itprovirt/thread/24ae635f-41a7-4c50-bcae-81cba3112b32)

トラブルシューティングしている掲示板を見つけた。レジストリで解決できるっぽいな。やっぱり原因はVISTAからUpgradeだったようだ。なんか他にもトラブルになりそうなところがあるかもしれないし、100% Windows 7 の性能を発揮できていないかもしれないので、クリーンインストールはしないといけないな。

～結果～

レジストリの修正では直らなかった。上記の掲示板の中に別の解決方法で、ウィザードを実行するexeファイルの場所が示されていたので、直接それを実行することでとりあえずの解決を得た。

Sun MicrosystemsのVirtual Boxもあるということなので、それもインストールしてみた。対応OSも多く、設定も簡単だった。UbuntuのISOイメージをダウンロードして、早速インストールしたが、解像度の変更に戸惑っている。コンフィグファイルを書かないといけないらしい。すんなりとは行かないな。