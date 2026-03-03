---
title: "Walkman Application in Sony Xperia Tablet S"
date: 2013-03-05T00:13:24+09:00
archives: ["2013-03"]
original_url: https://ameblo.jp/yuki9902/entry-11483640458.html
categories: ['COMPUTER']
---

Sony Xperia Tablet SにインストールされているWalkmanアプリは、DLNAに対応しています。  
  
DLNAサーバー（Windows Media SeverやDLNA対応HDDなど）に蓄積された音楽ファイルを再生することができます。  
  
WindowsアプリケーションのFoobar2000のUPnPサーバー機能を使って、再生することができます。  
... ただしストリーム形式はmp3じゃないといけません。  
ほかのDLNAクライアントと併用する場合は、Foobar2000側の設定で、Tablet用のプロファイルを作成します。  
Use profile when に「X-AV-Client-Info」を、containに「av=5.0; cn="Sony"; mn="SGPT12"; mv="2.0";」を設定します。  
Walkmanアプリは、バグがあるというか、DLNA仕様にそってないのか、Foobar2000とは相性が悪いです。  
プレイリストが表示されなかったり、再生できないプレイリストがあったり・・・。  
Foobar2000のマルチバイト文字列の扱いにバグがあるせいかもしれませんけれど。  
  
--Add 2013/03/06--  
  
ここにWalkmanアプリのDLNA仕様に正確に対応していないことが書かれています。  
シングルクォート「'」が、ファイル名やタイトル、アーティスト名などの文字列に含まれていると再生できないとことです。  
B'zの楽曲は無理と言うことに…。  
一度再生を失敗した楽曲情報は、Devicesに記録されてしまっているので、これのキャッシュと  
データを削除しないと再生できません。  
こんなヘルプを書くぐらいなら、改善をしてほしいモノです。  
--End--  
  
--Add 2013/04/22--  
4/18のアップデートで、Walkmanアプリの「'」シングルクォートの問題が改修されています。  
そのほかのバグも改修されています。  
電源落ちる問題、画面がフラッシュする問題など。  
--End--  
  
ほかにWalkmanアプリは「Throw」という機能があります。  
DLNA対応でWindows Media Playerのリモート再生に対応した機器(UPnPメディア機器)にデータを送信して再生することができます。  
データは、画像、音楽、動画などです。  
MacでいうところのAirPlayに近いでしょうか。  
このThrowを使うと、Walkmanアプリで再生操作するとWi-FiでつながったAVアンプから音が出ます。  
  
私の持っているAVアンプ(DENON AVC-4320)がWindows Media Playerのリモート再生に対応していることを初めて知ったのは、購入してから数年たったころでした。  
Windows VISTA認証機器ということは知っていたのですが・・・。  
マニュアルにも書いてなかったし、Windows Media Playerのヘルプにもそんなことが書いてなかったので判らなかったのです。  
あるときONKYOの製品紹介ページを見ているときに、Windows VISTA/7認証のAVアンプ製品のことが記述されていたので、同じくWindows VISTA/7の認証機器のDENON AVC-4320もできるはずと思って、Windows7からリモート再生したらできたのです。  
  
で、今日、WalkmanアプリからThrowをしてみたら、AVアンプから音が出ました。  
  
Android端末でできることが意外に多いです。  
ベースになったのはLinuxだから当たり前か…。  
  
しかしDLNAに関しては、知らないことが多すぎます。  
  
Sony Xperia スマートフォンを持っていてWalkmanアプリが使える場合は、Throwを試してみたらどうでしょうか。