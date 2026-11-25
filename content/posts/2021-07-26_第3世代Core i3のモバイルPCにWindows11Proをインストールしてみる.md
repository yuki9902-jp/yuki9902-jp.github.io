---
title: "第3世代Core i3のモバイルPCにWindows11Proをインストールしてみる"
date: 2021-07-26T14:40:44+09:00
archives: ["2021-07"]
original_url: https://ameblo.jp/yuki9902/entry-12688644675.html
categories: ['COMPUTER']
---

追記：2026/01/20 現在はWindows 11のハードウェア条件、TPM2とセキュアブートのチェックが無くなっています。

[『第3世代Intel Core i3 CPU環境へWindows 11をインストールする』第3世代Intel Core i3 CPU環境へWindows 11をインストールする1. はじめに：10年選手を現役へかつて「Windows 11は第8世代…!ameblo.jp![](https://stat.profile.ameba.jp/profile_images/44/yuki9902/1246028974083.jpg)](https://ameblo.jp/yuki9902/entry-12954754848.html)

　新しいOSは試してみたくなるのが元SEの性です。

　いずれ否応なく新しいOSに移行しなくてはいけなくなるものですし、Windows XP Professional x64、Windows VISTA Ultimate x64、Windows 7 Ultimate x64に乗り換えてきたときのようにOSを購入してから使えなくなる機器を確認するのではなく、前もって正式リリースの前に把握しておく必要があります。

　さて今回インストールするのは、Windows 11 Pro Developer Previewです。

　システム要件を満たすPCにインストールする場合は、Windows Insider Programで開発者アカウントを有効にすれば、Windows Updateから提供されるDeveloper Previewにアップグレード出来るようになります。

　今回インストールするPCはNEC VERSA Pro(NEC PC-VK24LFWDG)です。CPUはIntel Core i3 3110M(2.4GHz) 2コア4スレッド、メモリは4GB、Storageは2.5インチSSDです。

　UEFIとセキュアブートに対応しているもののTPM2には対応していません。したがってレジストリをいじってTPM2とセキュアブートのチェックを回避します。

　クリーンインストールしたいので、ブータブルUSBセットアップメディアを作成します。

[UUP dumpDownload UUP files from Windows Update servers with ease. This project is not affiliated with Microsoft Corporation.!uupdump.net![](https://uupdump.net/img/cover.png)](https://uupdump.net/)

 上記のリンクから、Latest Dev Channel Buildのx64のビルドファイルを任意のフォルダーにダウンロードします。

　zipファイルを解凍して、cmdファイルを管理者権限で実行します。cmdを実行したカレントフォルダーにいくつかのファイルがダウンロードされた後、ISOファイルが作成されます。

　次にRufusを使って、ISOファイルをUSBメモリに書き込みます。ISOファイルは5GB以上あるので8GB以上のUSBメモリを用意しましょう。

　書き込み終わったUSBメモリを目的のPCに挿して、BIOSからUEFIを有効にして、USBメモリからブートするように変更して再起動します。

　Windows11のセットアップ画面が表示されたらShift + F10を押してコマンドプロンプトを表示させ、Regedit.exeと入力してレジストリエディタを起動させます。

　\HKEY\_LOCAL\_MACHINE\SYSTEM\Setup\に新しくキー「LabConfig」を追加します。その中にDWORDで「BypassTPMCheck」16進数の値「1」と「BypassSecureBootCheck」16進数の値「1」を追加します。

　レジストリエディタを閉じ、コマンドプロンプトを閉じ、引き続きセットアップを続行します。

[![](/img/o1920108014977840793.jpg)](/img/o1920108014977840793.jpg)

一部ドライバーがインストールされていませんが、特殊なハードウェアが無ければ大体そのまま使える状態に成っています。

 Windows10のドライバーで問題ないと思われるので、ドライバーをインストールした後、試用していきたいと思います。

　タスクアイコンが中央に寄ったことでモバイルPCではかなり使いやすくなっていると思います。

　私はもともと左下のWindowsアイコンに機能が集中するのが好きではないので、今回のデザインは大いに賛成です。