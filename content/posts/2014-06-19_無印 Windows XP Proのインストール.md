---
title: "無印 Windows XP Proのインストール"
date: 2014-06-19T15:44:27+09:00
archives: ["2014-06"]
original_url: https://ameblo.jp/yuki9902/entry-11880709738.html
categories: ['COMPUTER']
---

32bitのWindows環境下でないと動作しないCanoScan 8000Fを使う必要に迫られたため、久しぶりに無印 Windows XP Professionalをインストールしてみた。

  

インストールしたのは、

CPU / AMD Phenom 9550 (Quad Core 2.2GHz 95W)

M/B / ASUS M3A32-Deluxe/Wi-Fi (AMD 790FX + AMD SB600)

Mem / 8GB (32bit環境下なので3.5GBまでしか使えない)

GPU / ASUS EN8600GT (nViDIA GeForce 8600GT 512MB)

HDD / WesternDigital Caviar Green 1.0TB

DVD / NEC DVDスーパーマルチドライブ

の自作PC。

  

さて、BIOS設定で、HDDの接続をAHCIからIDEに変更して、Windows XP ProfessionalのCD-ROMを起動。

20分もかからずWindows XP Professionalのインストールは完了。

  

M/Bに付属のDVD-ROMからドライバーをインストールしようとするもチップセット、サウンド、LANのドライバーはインストールできたが、USB2.0のドライバーがインストールできない。

  

Windows XP SP1以上が必要とのこと。

  

で、Windows XP SP1を適用しようと、Windows Updateにつなごうとしたが、Internet Explorer 6.0ではDNSエラーとなってしまう。

Microsoftの案内では、Internet Explorer 8.0をインストールするようにとでていたが、IE8のインストーラーが、無印Windows XP Professionalでは必要なDLLがないので、エラーを表示して終了する。

  

困ったので、Windows XP SP3をインストールしようとしたが、SP3は、SP1a以上が適用されていないと、インストールできない。

  

XP SP3以外のサービスパックのスタンドアローンインストーラーは、IE6からはどうやってもダウンロードできないので、ブラウザをGoogle Chromeにしてみようとするが、Chromeも必要なDLLがないので、インストールできない。

  

つまり、無印Windows XP Professional単体では、アップデートすることすらできず、完全に手詰まり。

サポート終了は、結構影響が大きいのだと再認識。

  
  

さて、メインに使っているPCはWindows 8.1 Pro with Media Centerなので、そちら側で、Windows XP SP2とSP3、ディスプレイドライバーなどをダウンロードして、共有フォルダーからWindows XPをアップデートした。

  

んで、Windows XP Pro SP3は使いづらいので、ライセンスを余らせていたWindows 7 Ultimate(32bit)に新規アップグレードした。

でもWindows 7 Ultimateのエクスプローラーも使いづらい。

  

さらにライセンスを余らせていたWindows 8 Proにアップグレードして、Windows 8 Pro with Media Centerに機能追加して、またさらに、Windows 8.1 Pro with Media Centerにアップグレードした。

  
  

Windows 8.1にアップグレードしたら、古いUSBキーボードが、英字配列キーボードとして認識されるトラブルが発生。

いろいろと対策をしてみたが、解決には至らなかった。

  

まあ、スキャナーマシンは、リモートデスクトップで使うので、マウスやキーボード、モニターが必要なわけではないので特段困らない。

  
  

しかし、AMD Phenom 9550についてきたリテールのCPUクーラーのファンの音がうるさい。