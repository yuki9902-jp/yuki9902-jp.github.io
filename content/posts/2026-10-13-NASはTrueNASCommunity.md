---
title: "NASはTrueNAS Community"
date: 2026-10-135T13:00:00+09:00
archives: ["2026-10"]
categories: ['COMPUTER']
tags: ['AMD','RYZEN','TrueNAS Community']
---
## はじめに

ファイルサーバーのデータ保護をファイルシステムの堅牢性の観点から検討した結果、ファイルサーバーをTrueNAS Communityで再構築しました。あわせて、リードキャッシュ用SSDの必要性を再検討したところ「不要である」との結論に至り、当該SSDはメインPCへと移設しました。

また、10年以上稼働させたTOSHIBA製3TB HDD 2台のうち1台が「代替処理済みセクタ数2,000カ所近く」という状態に陥り、プラッターに物理的な傷等が生じたものと判断して完全に引退させ、TOSHIBA製6TB HDD（HDWG760UZSVA）2台へと置き換えました。

## ファイルサーバーの構成

| **Item** | **Description** |
| ---: | --- |
| **OS** | TrueNAS Community |
| **CPU** | AMD Ryzen 7 3700X |
| **M/B** | ASUS ROG STRIX X570-F GAMING (AMD X570) |
| **RAM** | G.SKILL F4-3600C18D-16GTZN 16GB x2 (DDR4-3600CL18 8GB*4) |
| **GPU** | GigabyteGV-N1050OC-4GL (GeForce GTX 1050Ti 4GB) |
| **NVMe** | WD BLACK SN750 250GB (WDS250G3X0C-EC) |
| **SATA HDD** | 東芝 3.5" HDD 4TB (MN08ADA400E /JP) |
| **SATA HDD** | 東芝 3.5" HDD 4TB (MN08ADA400E /JP) |
| **SATA HDD** | 東芝 3.5" HDD 6TB (HDWG760UZSVA) |
| **SATA HDD** | 東芝 3.5" HDD 6TB (HDWG760UZSVA) |
| **NIC2** | RealTek PCIe 5GbE |
| **Uses** | Data Backup |

## 設定のポイント

1. BIOS
    1. Global C State : Disable
    2. PBO2/OC : Disable
    3. XMP2 : Enable

2. SMB
    1. MultiChannel : Enable

## ハードウェア選定

かつてメインPCで使用していたパーツを活用することで、イニシャルコストを0に抑えています。

よく「ECCメモリの導入」にこだわる声を聞きますが、宇宙線などの放射線によるシングルビットエラーや量子力学的トンネル効果といった極端なケースを除き、一般的なコンシューマー環境においてECCが必須となるシーンは多くありません。コンシューマー向けで「絶対にデータエラーが許されない処理」とは具体的に何か、一度立ち止まって考えてみる価値はあるでしょう。仮に書き込みファイルにエラーが生じたとしても、ZFSなどのチェックサム機能で検知・修復されるため、コンシューマー用途でECCメモリがマストになるケースは現実的ではないと考えます。

## 最後に

これまで、Windowsの「記憶域プール」と「ReFS」の組み合わせや、「XigmaNAS（FreeBSD系）」などを用いたファイルサーバーの構築・運用を経験してきました。

| OS | **Windows 11** | **XigmaNAS** | **TrueNAS Community** |
| :--: | :--: | :--: | :--: |
| **Base OS** | Windows 11 | FreeBSD | Debian |
| 構築難易度 | ◎ | × | ◎ |
| 堅牢性 | ◎ | ◎ | ◎ |
| セキュリティー | ◎ | △ | ○ |
| 運用性 | ◎ | × | ◎ |
| **FileSystem** | 記憶域プール & NTFS / ReFS | XFS | XFS |
| 堅牢性 | NTFS:× / ReFS:○ | ◎ | ◎ |
| 運用性 | △ (PowerShell必須) | △ | ◎ |
| 速度 | △ | ◎ | ◎ |

様々な検討を重ねた結果、最終的にTrueNAS Communityを選択するに至りました。
