---
title: "XigmaNASからTrueNAS Community Editionへ"
date: 2026-03-10T12:00:00+09:00
archives: ["2026-03"]
categories: ['COMPUTER']
tags: ['AMD','Ryzen','1700','GIGABYTE','X370','TrueNAS','SMB3','MULTICHANNEL']
---

## 1. はじめに

TrueNAS Coreが終了したのでXigmaNASに乗り換えましたが、セットアップ、運用の手間が結構大変なこともあって、万が一トラブった場合も復旧が簡単なNAS OSがないかと探していました。運用の手軽さだけなら、TrueNAS Community Editionがあったんですが、ARCキャッシュの持ち方がFreeBSD系のTrueNAS Coreと違って、ファイル更新分のチェックをするのにHDDを再帰検索してしまうので遅さに困っていました。ですが、NVMe SSDを使ってL2ARCキャッシュのディスクにすると遅さを解消できるということを知りました。余っていたNVMe SSD 2枚をL2ARCキャッシュ用に、240GB SATA SSDをOSインストール用に用意して、TrueNAS Community Editionをインストールすることにしました。TrueNAS Community Edition (旧Scale) はマシンを再起動してもL2ARCキャッシュが維持されるため、再起動後のアクセスも高速に行えるメリットがあるので、NASを使わないときに電源を落としている私には有用です。

## 2. 構築目標

1. 3TB HDDx2のミラー、4TB HDDx2のミラーで、プールを二つ作る。
2. ミラープール毎にL2ARC用のNVMeを一台ずつ割り当てる。
3. SMB3でWindows用ファイル共有をする。
4. 192.168.11.11/24 192.168.22.22/24を設定する。
5. デフォルトゲートウェイ、DNSは192.168.11.1を設定する。
6. SMB3 Multichannel接続を設定し、1GbEx2で2Gbps転送を実現する。

## 3. 環境

| Device | Product |
| ----- | ----- |
| CPU | AMD Ryzen 7 1700 (8C/16T) |
| RAM | DDR 2666MHz CL16 32GB (16GBx2) |
| M/B | GIGABYTE GA-AX370 Gaming K7 (AMD X370) |
| SATA SSD | ADATA SP900 240GB |
| NVMe SSD | WD NVMe SSD 512GB (WDC WDS512G1X0C-00ENX0) |
| NVMe SSD | WD BLACK SN750 250GB (WDS250G3X0C-00SJG0) |
| HDD | TOSHIBA DT01ACA300 3TB x2 |
| HDD | TOSHIBA MN08ADA400E 4TB x2 |

## 4. 構築
### 1. インストールメディア
- [TrueNAS](https://www.truenas.com/)からProductのTrueNAS Community Editionを選んでisoファイルをダウンロードする。
- Balena EtcherからUSBメモリにダウンロードしたisoファイルを書き込む。

### 2. インストール
- BIOSの設定
    - Global C State Control : Disable
    - UEFIブート
    - HD Audio Device : Disable

- USBメモリを差し込んで起動
    - TrueNAS Installを選択
    - インストール先にADATA SP900を選択

### 3. ネットワーク設定
- `1) Configure network interfaces`を選択
    - IPv4、IPv6のDHCPをオフにする。
    - Aliasを選び 192.168.11.11/24と192.168.22.22/24を設定する。

- `2) Configure network settings`を選択
    - DefaultGatewayに192.168.11.1を設定。
    - DNSに192.168.11.1を設定。
    - Host NameにSURVIVEを設定。
    - Domain NameにYSを設定。

### 4. WebUIからのセットアップ

### 4-1. 基本設定

- 「システム」の「一般的な設定」の「ローカライゼーション」の「設定」ボタンをクリック
    - 言語 : Japanese
    - キーボード : Japanese
    - Time zone : Asia/Tokyo

- 「保存」をクリックする。
    - 一項目ずつしか保存されない場合があります。再起動を繰り返しながら一項目ずつ設定してください。

### 4-2. Poolの作成

1. Pool_3TB (3TBミラー)
    1. ストレージダッシュボードの「プールの作成」ボタンをクリック。
    2. 名前をPool_3TBとする。
    3. Mirrorを選択、ストレージは3TB HDDを選択。
    4. 6項目目Cacheにストレージ NVMe 250GBを選択。

2. Pool_4TB (4TBミラー)
    1. ストレージダッシュボードの「プールの作成」ボタンをクリック。
    2. 名前をPool_4TBとする。
    3. Mirrorを選択、ストレージは4TB HDDを選択。
    4. 6項目目Cacheにストレージ NVMe 500GBを選択。

### 4-3. DataSetの作成

1. Pool_3TBを選んで「データセットを追加」をクリックする。
    1. データセット名を「Data_3TB」にし、「データセットのプリセット」を「SMB」にする。
    2. 「保存」をクリックする。

2. Pool_4TBを選んで「データセットを追加」をクリックする。
    1. データセット名を「Data_4TB」にし、「データセットのプリセット」を「SMB」にする。
    2. 「保存」をクリックする。

### 4-4. 共有の設定

- SMB
    - NetBIOS名 - SURVIVE
    - WORKGROUP - YS
    - 詳細をクリックし、Multichannelのチェックボックスをオンにする。

- SMBの設定を保存する。

- 「共有」のSMBサービスに作成したデータセットが含まれているのを確認する。

- 「システム」の「サービス」の「SMB」を開始し、「自動的に起動」をオンにする。

#### 4-5. 認証情報

- 「ユーザー」をクリック
- 「追加」をクリック 
    - 「ユーザー名」を入力し
    - 「SMBアクセス」にチェック
    - 「パスワード」と「パスワードの確認」に入力
- 「保存」をクリックする。

### 5. 接続確認

1. Windows上のエクスプローラーのアドレスタブに、`\\192.168.11.11` もしくは `\\192.168.22.22` もしくは `\\SURVIVE`と入力する。
2. ユーザー認証画面に4-5.で作成したユーザー名とパスワードを入力してログインする。
3. Data_3TB、Data_4TBが表示され、フォルダにアクセス出来ていれば成功。
4. マルチチャンネル接続の確認はWindows PowerShellを開いて以下のコマンド入力して確認。
```PowerShell
Get-SmbMultichannelConnection
```

コマンドの結果
```
Server Name   Selected Client IP      Server IP     Client Interface Index Server Interface Index Client RSS Capable Client RDMA Capable
-----------   -------- ---------      ---------     ---------------------- ---------------------- ------------------ -------------------
192.168.11.11 True     192.168.22.222 192.168.22.22 12                     3                      False              False
192.168.11.11 True     192.168.11.156 192.168.11.11 7                      2                      False              False
192.168.22.22 True     192.168.22.222 192.168.22.22 12                     3                      False              False
192.168.22.22 True     192.168.11.156 192.168.11.11 7                      2                      False              False
SURVIVE       True     192.168.22.222 192.168.22.22 12                     3                      False              False
SURVIVE       True     192.168.11.156 192.168.11.11 7                      2                      False              False
```