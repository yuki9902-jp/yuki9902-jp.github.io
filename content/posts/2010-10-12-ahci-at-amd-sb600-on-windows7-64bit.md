---
title: "AHCI at AMD SB600 on Windows7 64bit"
date: 2010-10-12T15:00:03+09:00
archives: ["2010-10"]
draft: false
categories: ['COLUMN', 'COMPUTER']
tags: []
---

ここ数年PCの勉強してなかったら、M/Bの能力を引き出すことを全く忘れてました。

SATA2のHDDを購入したのを機にもうちょっと出来ることがあるんではないのかとBIOSを見ていると、SATAの項目の中にAHCIがありました。
SATA2対応ディスクの性能を引き出すためには、設定してほうが良いらしいとのことだったので、AHCIに設定して、Windows7を起動させようとしました。

すると起動時にクラッシュして、復元モードが起動しました。
しかも復元モードも途中で、「復元できませんでした」と表示されます。

まあさっぱり勉強していなかったので仕方ないです。

とりあえずSATA設定をIDEに戻して再起動すると、Windows7が起動できました。
インターネットでAHCIについて調べてみると、IDEモードでインストールしたWindows7/VISTAをAHCIモードにして起動した場合、クラッシュすると書かれていました。
それからIDEモードでインストールした後にAHCIモードにする方法がありました。

[AHCIモード - Windows7移行まとめwiki](http://windows7.wiki.fc2.com/wiki/AHCI%E3%83%A2%E3%83%BC%E3%83%89)

先のリンク先の説明はIntelのチップセット。
私の持っているのはAMDのSB600なので、[AMDのサイトからAHCI用のドライバー](http://support.amd.com/us/gpudownload/windows/Pages/raid_windows.aspx)をダウンロードします。
***注*** Windows 7の標準ドライバのほうが良いようで、AMDからSB600用のACHIドライバの配布はなくなりました。
上記のリンクにはSB700以降のドライバがあります。

次にレジストリを変更。レジストリエディタを起動し、

HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Msahciのサブキーを選択。

「Start」の数値を3から0に変更し保存しまう。
（数値が4の場合なども有り）

Windows7を再起動させて、BIOSでSATAをAHCIモードに設定して、起動。
Windows7が起動するとHDDなどを再認識して、ドライバーを再構成。
また再起動。
そしてAMDのAHCIドライバーをインストールして再起動。

ついでにサウスブリッジのドライバーもインストールしておきます。

CrystalDiskMarkで速度を計測しましたが、シーケンシャルアクセスでは
１％以内の差があるかどうかです。
random accessでも5%も差が無いようです。
まあ、最大性能を出したと言うことで良しとしましょう。

で、AHCIモードでWindowsVISTAをインストールするにはWindowsの修正プログラムを適用したSP1が必要だそうです。
Windows7については分からないです。
WindowsXPについてはドライバーディスクを用意しておく必要があるそうです。
IDEモードでインストールしたあとにAHCIモードに切り替えた方が簡単かも。