---
title: "悲報、Windows11はAMDのCPUだと最大25％のFPSダウン･･･"
date: 2021-10-08T00:49:09+09:00
archives: ["2021-10"]
original_url: https://ameblo.jp/yuki9902/entry-12702447062.html
categories: ['COMPUTER']
---

Windows11での検証をYoutubeのPC系のニュース動画で報告していたんですが、VBS(Virtualization-based Security)仮想化ベースのセキュリティー機能により、ゲームのパフォーマンス、FPSにして最大25％ダウンすることが分かりました。

　これはTPM2のサポート以外のCPUに対して制約として、Ryzen1000シリーズ（Zen Core）が非対応になったし、AMDにも詳細に検証して貰ってもWindows11を完全には動かせないことが確認されています。

　10月5日からWindowsUpdateを通して、Windows11のアップグレードが可能になっていますが、問題が解消されるまで導入は見送ります。

　正規リリースでは、仮想化とマルチスレッドの予測分岐の方法が完全に見直されているので、Windows10のアップグレードではなく全く別のOSとして検証が必要です。Windows10ベースで最適化してあるアプリケーションでは予期しない性能ダウンを引き起こすと思われるので、開発者にはかなり厳しい更新になります。

　GUIのカスタマイズ制限も厳しいので、やっぱりこの世代のWindowsはMe、XPx64、VISTA、8、8.1と同じ運命をたどるんでしょうね。