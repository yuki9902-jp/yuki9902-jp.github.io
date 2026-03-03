---
title: "Garuda Mokkaに移行に挑戦したものの"
date: 2026-02-24T13:13:14+09:00
archives: ["2026-02"]
original_url: https://ameblo.jp/yuki9902/entry-12957745524.html
categories: ['COMPUTER']
---

メインPCのOSをGaruda Mokkaに移行しました。

いい加減、Microsoft、Adobeのユーザー指向ではないビジネスモデルにうんざりしてきていたので。  
  
Adobe Photoshopはフォトエディションを途中解約したので違約金が9000円ほど盗られました。契約に承諾していないのに違約金が発生する契約を結ばされていたのは完全に商法違反、消費者保護法違反ですが、争うのが面倒なので、勉強料だと思って我慢します。

Gemini 3 Flashと相談しながら各種設定作業を進めています。  
  
・インストール

・Mozc日本語設定

・7.1chオーディオ構成

・Thunderbirdのバックアップからの復元

・RAID0を含むドライブ構成

・NIC2つのネットワーク構成

・SAMBAとSMB3マルチチャンネル接続設定  
・XigmaNASからのバックアップデータ復元

データ復元中なのでしばらく掛かりそうです。

このあとは、

・ROCmのインストール  
・ComfyUIのインストール

・学習済みモデルのバックアップデータからの復元

・Corsair iCue Linkの設定

・Elgato Stream Deckの設定

・Elgato Face Camの設定

と作業を進めていく予定です。

2026/02/25  
・ROCm7.1.xのインストールを行う。  
・ComfyUIのインストールを行う。

ComfyUIを実行中、KSmaplerが動き出す直前で、GPUがハングアップを起こし、Geminiに頼りながら解決策を数時間にわたり模索しましたが、解決には至りませんでした。

もろもろの設定の難しさ、最新ハードウェアに対応できないことからGaruda Mokkaをあきらめ、Windows 11 Proに戻しました。