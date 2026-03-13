---
title: "Windows環境のRadeon RX 9070 XTでComfyUIを使う 2026/1/24"
date: 2026-01-24T06:34:51+09:00
archives: ["2026-01"]
original_url: https://ameblo.jp/yuki9902/entry-12954404367.html
categories: ['COMPUTER']
tags: ['RADEON','RX9070XT','ComfyUI','ROCm','Windows11Pro']
---

### 1. はじめに

2025年末から2026年1月にかけて、AMDユーザー待望のAI環境がかなり整いました。**Radeon Software:Adrenaline 25.20.01.17 with ROCm7.1.1 Pytorch** の公開と、さらに2026年1月21日に公開された **AMD Software: Adrenalin 26.1.1 AIbundle** により、Windowsネイティブ環境でのAI生成（ComfyUI）が、かなり簡単になりました。（注意：Ollamaの設定は難しいままです。）

現時点における「2026年1月の簡単導入手順」を提供します。

---

### 2. 構築環境（2026年1月時点）

最新のRDNA 4アーキテクチャとROCm 7.xを活かすための構成です。

| **項目** | **要件 / 使用パーツ** |
| --- | --- |
| **GPU** | **ASUS TUF-Gaming RX 9070 XT OC 16GB** (RDNA 4) |
| **CPU** | **AMD Ryzen 9 9950X3D** (CPUの処理も行われるので良いものを) |
| **RAM** | **DDR5-6000 64GB** (32GB以上を強く推奨) |
| **OS** | **Windows 11 Pro 25H2** |
| **Driver** | **Adrenalin 26.1.1 (AI Bundle同梱版)** |

#### **【重要】メモリの最低要件**

メモリ高騰の中、非常に苦しい要件ですが、メインメモリは32GBを用意してください。最新の巨大なAIモデル（FLUX.1等）を扱う場合、16GB環境ではモデルのロード時や高解像度化の際にプロセスが強制終了（クラッシュ）する事例が多発しています。安定運用のための「実用上の最低ライン」として32GB以上を推奨しています。

#### **【重要】UEFI（BIOS）設定**

導入前に必ず以下が「Enable（有効）」であることを確認してください。これらがオフだと、AI処理のパフォーマンスが著しく低下、または起動しません。

* **Above 4GB Decoding**
* **Resizable BAR**

---

### 3. インストール手順

**ステップ1：AI Bundle対応ドライバの導入**

[AMD公式サイト]より **Adrenalin 26.1.1** 以降をダウンロードします。

1. インストール時のカスタムオプション、または追加コンポーネント選択で **「AI Bundle」** にチェックを入れます。
2. これにより、**ROCm 7.1.1、PyTorch、およびComfyUIのベース環境**がシステムと隔離された形で自動インストールされます。

#### **ステップ2：Git版ComfyUIのセットアップ（詳細制御したい場合）**

[AMD ROCm Software for Radeon and Ryzen](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.1.1/index.html) ドライバに同梱されているROCmのバージョンを確認してください。このリンクは7.1.1です。

1. [Install PyTorch via PIP](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.1.1/docs/install/installrad/windows/install-pytorch.html#install-pytorch-via-pip) に従いPyTorchをインストールします。
2. [Install ComfyUI](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.1.1/docs/advanced/advancedrad/windows/comfyui/installcomfyui.html#install-comfyui) に従いComfyUIをインストールします。  
   ComfyUIをGitから取得してください  
   ```bash {.copy}
   git clone https://github.com/comfyanonymous/ComfyUI.git
   ```
   カレントフォルダを移動します。  
   ```bash {.copy}
   cd \ComfyUI
   ```
   以下を入力し、インストールしてください。  
   ```bash {.copy}
   pip install -r requirements.txt
   ```

---

### 4. モデル管理の最適化（Stability Matrixとの連携）

複数のUI（Stable Diffusion web UI / Amuse等）を併用する場合、モデルデータの重複はSSDを圧迫します。

1. **Stability Matrix** のGUIが優れているので、共通のモデル管理サーバーとして利用します。
2. Stability Matrix上でComfyUIをインストールします。
3. Stability Matrixのインストールフォルダにある  
   `..\data\packages\ComfyUI\extra_model_paths.yaml`  
   を、本環境のComfyUIフォルダへコピー。
4. YAMLファイルをテキストエディタで開き、ComfyUIからの相対パスまたは絶対パスをStability Matrixの\Data\Modelsフォルダにしてください。
5. Stability Matrix上のComfyUIは必要ないのでアンインストールします。
6. これで**Stability MatrixのGUIを使った****、巨大なモデル（FLUX.1や最新のSD3.5等）の一元管理**が可能になります。

---

### 5. 以前の環境との比較

前環境では、RYZEN 9 5900XTおよびRYZEN 7 5800Xとメモリ64GB、RADEON RX6750XTに、ComfyUI-ZLUDAを苦労してインストールして運用していました。SDXLの学習済みモデルを使い42ステップで1080\*1528の元画像作成し、モデルを使ったアップスケーリングで4000\*6000相当の画像を作成するのに300秒強を要していました。  
現環境のRYZEN 9 9950X3D、メモリ64GB、RADEON RX 9070XTに、ROCm7.1.1とComfyUIの運用では、同じ条件の画像作成で95秒と約3分の1に時間を短縮できています。特にGPUの世代と性能が大きく寄与しています。今後の環境構築の参考にしてください。

---

### 6. おわりに

長らくAMD RADEONでAIは敷居が高かったのですが、RX 9070 XTとAdrenaline 26.1.1ドライバの登場で、非常に簡単になりました。手前の環境の**ASUS TUFモデル** や、他社の**Taichiモデル** のような大きなヒートシンクと強力なファンの冷却機構を持つボードでは、長時間の生成でもホットスポット温度が安定しやすく、ComfyUIを安心して長時間使うことができます。

ハードウェア高騰が続く中、VRAM 16GBを搭載し、ネイティブROCm対応を果たしたRX 9070 XTも価格上昇を免れませんが、2026年のAI PC自作における「手の届きやすい選択肢」と言えるでしょう。