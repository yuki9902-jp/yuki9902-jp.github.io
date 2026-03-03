---
title: "VB-Audio VoiceMeeter Potato"
date: 2020-09-06T00:08:33+09:00
archives: ["2020-09"]
original_url: https://ameblo.jp/yuki9902/entry-12622831000.html
categories: ['COMPUTER']
---

[VB-Audio Software](https://www.vb-audio.com/index.htm)のVoice Meeter Potatoをインストールしました。

[![](https://stat.ameba.jp/user_images/20200905/23/yuki9902/5c/1c/p/o1645077014815168981.png?caw=800)](https://ameblo.jp/yuki9902/image-12622831000-14815168981.html)

WindowsとMac用のオーディオミキサーです。

Windows 10にインストールしました。

[![](https://stat.ameba.jp/user_images/20200905/23/yuki9902/5a/83/p/o0465051814815170454.png?caw=800)](https://ameblo.jp/yuki9902/image-12622831000-14815170454.html)

[![](https://stat.ameba.jp/user_images/20200905/23/yuki9902/15/c4/p/o0465051814815172746.png?caw=800)](https://ameblo.jp/yuki9902/image-12622831000-14815172746.html)

サウンド設定でVoiceMeeter Inputというバーチャルハードウェアを選択して既定値に設定、構成を7.1チャンネル、プロパティの規定の形式を24ビット、192000Hz(スタジオの音質）に設定します。

次にVoiceMeeter Potatoを起動して、Virtual InputsでVoiceMeeter VAIOの出力先をA1に設定、Hardware OutのA1をプルダウンして、WDM(WASAPI)のRealtek Audioを選択します。

他にサウンド関係のハードウェアをつないでいる場合には、A2、A3、A4、A5に設定していきます。

ハードウェアに応じて、WDM(WASAPI)、KS(カーネルストリーミング)、MME(DirectX)、ASIOのAPIもしくはドライバを選択することが出来ます。

Windows 10ではWDMかASIOを選択すると思います。

ASIOを使う場合はA1に割り当ててください。

VoiceMeeterのMenuから設定できるWDM、ASIOともバッファリングの値は小さい方が良いみたいです。

LANを通してオーディオをストリームする機能のVBANの送出側で音飛びが発生します。

他にSony PHA-1Aというポータブルアンプ（USB-DAC）をつないでいるんですが、このASIOドライバー側のバッファは2msに設定しても問題なく音が鳴りました。

ノートPCにもVoiceMeeterをインストールしてVBANを使ってみました。

前述したようにバッファリングの値が初期値だと音飛びが発生しました。

あとサンプリングレートが44.1kHz系統か48kHz系統かの違いでも音飛びが発生します。

受信側が48kHz系統の倍数、48kHz、96kHz、196kHzをHardware Outに設定していると、送出側で44.1kHzのデータを送ると音飛びが発生しました。

96kHz、24bit、8ch(7.1ch)を送出すると50Mbps程度のトラフィックが流れます。

有線LANで接続した方が良いでしょう。

まだゲームでは試していないので、どれくらいCPUに負荷が掛かり、遅延が発生するか調べていません。

通常の音楽再生ソフトでは気になりません。

マイク入力から音が出るまでには50ms程度の遅延が発生します。

安価にOBSなどで配信したい場合などは良いかもしれませんが、本格的に使う場合はASIOに対応した外部のハードウェアミキサーを購入した方が良いと思います。