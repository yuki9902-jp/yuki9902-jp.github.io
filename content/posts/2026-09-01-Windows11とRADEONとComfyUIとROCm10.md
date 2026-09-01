---
title: "ComfyUIをRADEON RX9070XT(ROCm10.0.0)とWindows11Pro 25H2の環境で動かす"
date: 2026-09-01T16:00:00+09:00
archives: ["2026-09"]
categories: ['COMPUTER']
tags: ['RADEON','RX9070XT','ComfyUI','ROCm','Windows11Pro']
---
## 1.始めに

2026/08/26にAMDからROCm10.0.0がリリースされました。ROCm10.0.0の動作要件は、AMD RadeonのドライバースイートであるAMD Software: Adrenaline Edition 26.6.4 (WHQL Recommended)です。
既にROCm7.14とROCm7.2.1での環境を作っていますが、ROCm7.14はアンインストールしてください。

## 2.環境

### ハードウェア

| Device | Product |
| --- | --- |
| CPU | AMD Ryzen 9 9950X3D |
| M/B | ASUS ROG STRIX X870E-E GAMING WIFI (AMD X870E) |
| RAM | Corsair CMH64GX5M2B6000Z30 (DDR5-6000 64GB) (32GB or more recommended) |
| GPU | ASUS TUF Gaming Radeon RX 9070 XT OC Edition 16GB GDDR6 |
| SSD | WD BLACK SN850X 2TB (NVMe Gen.4x4) System (C:) |
| SSD | WD BLACK SN850X 2TB (NVMe Gen.4x4) ComfyUI (D:) |

### ソフトウェア

| Software | Product |
| --- | --- |
| OS | Microsoft Windows 11 Pro 25H2 |
| Chipset Driver | AMD Chipset Drivers 8.01.20.513 |
| GPU Driver | AMD Software: Adrenalin 26.6.4 (WHQL Recommended) |
| Interpreter | Python 3.12.10 Windows installer (64-bit) |
| Interpreter | Python 3.12.10 Windows embeddable package (64-bit) |
| AI Suite | Stability Matrix |
| AI Generator | ComfyUI (Git) |

### BIOS (UEFI)

以下はメインメモリとVRAMのやりとりをスムーズにするため必須です。

- Avobe 4G Decoding : Enable
- ReSizable BAR : Enbale

以下はWHEA-Logger ID:18とCPU焼損対策です。 (OCと省電力機能を無効)

- Global C State : Disable
- PBO2 : Disable
- EXPO I
- SoC/UnCore : Disable

## 3.インストール

### GPU Driver

#### [AMD Software: Adrenalin Edition 26.6.4 Driver Release Notes](https://www.amd.com/en/resources/support-articles/release-notes/RN-RAD-WIN-26-6-4.html)

上記のリンクからダウンロードし、インストールしたら念のためPCを再起動します。

### Python 3.12.10

[Python 3.12.10](https://www.python.org/downloads/release/python-31210/)をダウンロードしてインストールします。

### ROCm10.0.0

1. ROCm7.14.0のアインストール

    管理者権限でコマンドプロンプトを起動し、ROCm7.14をインスト-ルした作業ディレクトリに移動します。

    ```Shell
    pip cache purge
    rmdir /s /q .venv
    ```

2. AMD ROCm 10.0.0のインストール

    **[Install AMD ROCm 10.0.0](https://rocm.docs.amd.com/en/latest/install/rocm.html?fam=radeon&w=compute&os=windows&windows-ver=11&i=pip&gpu=amd-radeon-rx-9070-gre&gfx=gfx1201)**

    管理者権限でコマンドプロンプトを起動します。

    1. 作業ディレクトリに移動します。

        ```shell
        D:
        ```

    2. Pythonの仮想環境を設定します。

        ```shell
        py -3.12 -m venv .venv
        ```

    3. .venvを有効化します。

        ```shell
        .venv\Scripts\activate
        ```

    4. ROCm 10.0.0をインストールします。

        ```shell
        python -m pip install --index-url https://stable.repo.amd.com/rocm/whl-next/ "rocm[libraries,device-gfx1201]==10.0.0"
        ```

3. PyTorch for ROCmのインストール

    **[Install PyTorch for ROCm 10.0.0](https://rocm.docs.amd.com/projects/ai-ecosystem/en/latest/frameworks/pytorch/install.html?fam=radeon&gpu=amd-radeon-rx-9070-gre&os=windows&rocm-ver=10.0.0&pytorch-ver=2.12.0&i=pip&w=compute&gfx=gfx1201)**

    管理者権限でコマンドプロンプトを起動します。

    1. 作業ディレクトリに移動します。

        ```shell
        D:
        ```

    2. Pythonの仮想環境を設定します。

        ```shell
        py -3.12 -m venv .venv
        ```

    3. .venvを有効化します。

        ```shell
        .venv\Scripts\activate
        ```

    4. ROCmを有効にしたPyTorchをインストールします。

       ```shell
        python -m pip install --index-url https://stable.repo.amd.com/rocm/whl-next/ "torch[device-gfx1201]==2.13.0+rocm10.0.0" "torchvision[device-gfx1201]==0.28.0+rocm10.0.0" "torchaudio==2.11.0.2+rocm10.0.0"
       ```

    5. PyTorchのインストールを確認します。

        ```shell
        python -c "import torch; print(torch.cuda.is_available())"
        ```

4. ComfyUIのインスト-ル

    [ComfyUI image generation on ROCm](https://rocm.docs.amd.com/projects/ai-ecosystem/en/latest/inference/comfy.html) に従いComfyUIをインストールします。(通常のGit版のComfyUIのインストールです。ROCm環境だからと言って特別な方法ではありません。)

    1. 管理者権限でコマンドプロンプトを起動し、カレントフォルダーをインストールしたい一つ上のフォルダに移動します。

        ```shell
        D:
        ```

    2. Pythonのvenv仮想環境を有効にします。

        ```shell
        D:\.venv\Scripts\activate.bat
        ```

    3. ComfyUIをGitから取得してください。

        ```bash
        git clone https://github.com/comfyanonymous/ComfyUI.git
        ```

    4. カレントフォルダを移動します。  

        ```shell
        cd \ComfyUI
        ```

    5. 以下を入力し、インストールしてください。  

        ```shell
        pip install -r requirements.txt
        ```

    6. ComfyUIを起動します。

        ```shell
        python main.py
        ```

    7. 起動が確認できたら、`Ctrl + C`でComfyUIを終了します。

    8. Pythonのvenv仮想環境を終了します。

        ```shell
        deactivate
        ```

### Stability Matrix

GUIが使いやすいため、これで学習済みモデルを一元管理するためにインストールします。

1. [Stabiolity Matrix](https://lykos.ai/downloads)をダウンロードし任意のフルダーで解凍します。
2. DドライブにSMフォルダー（任意ですが、マルチバイト文字や空白が含まれると不整合の対策に悩まされる）を作成し、解凍したStabilityMatrix.exeを入れます。
3. StabilityMatrix.exeをダブルクリックし起動します。
4. StabilityMatrix上で、ComfyUI（ComfyUI-ZLUDAじゃないほう）をインストールします。
5. `D:\SM\Data\Packages\ComfyUI\extra_model_paths.yaml`が必要なので、コピーして`D:\ComfyUI\`にペーストします。
6. StabilityMatrix上のComfyUIは必要ないのでアンインストールします。
7. extra_model_paths.yamlの内容を編集します。

   #### extra_model_paths.yaml

    ```yaml
    stability_matrix:
    base_path: D:\SM\Data\Models\
    checkpoints: StableDiffusion
    diffusers: Diffusers
    loras: |-
        Lora
        LyCORIS
    clip: TextEncoders
    clip_vision: ClipVision
    embeddings: Embeddings
    vae: VAE
    vae_approx: ApproxVAE
    controlnet: |-
        ControlNet
        T2IAdapter
    gligen: GLIGEN
    upscale_models: |-
        ESRGAN
        RealESRGAN
        SwinIR
    hypernetworks: Hypernetwork
    ipadapter: |-
        IpAdapter
        IpAdapters15
        IpAdaptersXl
    prompt_expansion: PromptExpansion
    ultralytics: Ultralytics
    ultralytics_bbox: Ultralytics/bbox
    ultralytics_segm: Ultralytics/segm
    sams: Sams
    diffusion_models: DiffusionModels
    ```

### 起動用バッチファイル

実用例として起動時の日付で出力先フォルダに日付フォルダを作成します。

#### ComfyUI_Date.bat

```bat
@echo off
setlocal

rem PowerShellを使って確実に yyyyMMdd を取得（ロケールに左右されません）
for /f "usebackq" %%i in (`powershell -NoProfile -Command "Get-Date -Format 'yyyyMMdd'"`) do set yyyymmdd=%%i
 
rem Get the Output path
set parentPath=F:\output
    
rem Create the folder with the name yyyymmdd
set outpath=%parentPath%\%yyyymmdd%
    
rem --- ROCm / PyTorch 最適化設定 ---
SET PYTORCH_HIP_ALLOC_CONF=garbage_collection_threshold:0.6
SET PYTORCH_HIP_ALLOC_CONF=expandable_segments:True
SET ROCM_ENABLE_PREFETCH=1
    
rem フォルダが存在しない場合のみ作成
if not exist "%outpath%" mkdir "%outpath%"
    
echo Target path: %outpath%
     
D:
call D:\.venv\Scripts\activate.bat
cd D:\ComfyUI
    
python main.py --output-directory %outpath% --preview-method none --reserve-vram 0.0 --cache-lru 8 --use-pytorch-cross-attention
endlocal
```

## 4.確認

1. Stability Matrixで使いたい学習済みモデルをダウンロードしてください。
2. ComfyUIを起動して、先ほどダウンロードした学習済みモデルが表示されれば成功です。

## 5.過去の環境との比較

**条件** SDXL学習済みモデル、1080x1528画像、30ステップ

| GPU | AI | Time (s) |
| --- | --- | --- |
| ASUS TUF Gaming Radeon RX 9070 XT OC Edition 16GB GDDR6 | ComfyUI + ROCm7.2.1 | 15 |
| ASUS TUF Gaming Radeon RX 9070 XT OC Edition 16GB GDDR6 | ComfyUI + ROCm7.14 | 15 |
| ASUS TUF Gaming Radeon RX 9070 XT OC Edition 16GB GDDR6 | ComfyUI + ROCm10.0.0 | 15 |

Windowsネイティブ環境で、かなり良い感じで生成できます。GeForce環境がないので比較はしたことありませんが、そこそこいけるレベルではないでしょうか。

## 6.画像を4倍に拡大する

ComfyUIの中で画像を生成し、そのまま拡大させると実VRAMが足りずに仮想VRAMとして割り当てたメインメモリにスワップします。そのときに非常に処理が遅くなるので、ComfyUIで生成と拡大を連続して処理するのはお薦めしません。さらにComfyUIは既に作成済みの画像ファイルを読み込んで拡大処理をするのにも適していません。カスタムノードマネージャーから該当のカスタムノードを追加する必要があり、また処理も速くありません。

そこで、Real-ESRGAN-GUIをインストールして画像ファイルの拡大処理を外部アプリに分散させます。このアプリでの処理ならComfyUIでの処理の約1/3の時間で拡大できます。

[Real-ESRGAN-GUI](https://github.com/tsukumijima/Real-ESRGAN-GUI)

## 7.最後に

Windows11 25H2、AMD RADEON RX9070XT(16GB)、ComfyUI、ROCm10.0.0の環境で、上手く処理させれば一日で約5000枚の画像を生成することができます。
{xxx|yyy|zzz}の構文をプロンプトに使えばランダム性を持たせられるので、狙った一枚を生成させるか、ランダムに大量生成させて気に入った一枚を見つけ出すかは使い方次第です。
