---
title: "ComfyUI/ROCm7.2/RX9070XT/Windows11Pro 25H2"
date: 2026-03-05T12:00:00+09:00
archives: ["2026-03"]
categories: ['COMPUTER']
tags: ['RADEON','RX9070XT','ComfyUI','ROCm','Windows11Pro']
---
## 1.始めに

2026/02/26にAMDからRadeonのドライバースイートである、AMD Software: Adrenaline Edition 26.2.2 (WHQL Recommended)が公開されました。前回の26.2.1 OptionalからROCm7.2が同梱され、ドライバーと共にインストールされます。
今回はWindows11Pro 25H2をクリーンインストールしたことを機にComfyUI (Git版)の環境を再構築しました。



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
| GPU Driver | AMD Software: Adrenalin 26.2.2 (WHQL Recommended) |
| Interpreter | Windows installer (64-bit) |
| Interpreter | Windows embeddable package (64-bit)|
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

### Windows 11 Pro 25H2

特に注意点はありません。画面に表示される手順でインストールします。

### Chipset Driver

[AMD Ryzen™ Chipset Driver Release Notes 8.01.20.513 ](https://www.amd.com/en/resources/support-articles/release-notes/RN-RYZEN-CHIPSET-8-01-20-513.html)

上記のリンクからダウンロードし、インストールしたらPCを再起動します。

### GPU Driver

[AMD Software: Adrenalin Edition 26.2.2 Release Notes](https://www.amd.com/en/resources/support-articles/release-notes/RN-RAD-WIN-26-2-2.html)

上記のリンクからダウンロードし、インストールしたら念のためPCを再起動します。

### Python 3.12.10

Adrenaline 26.2.2をインストールするときに一緒にインストールされるはずです。

されていない場合は、[Python 3.12.10](https://www.python.org/downloads/release/python-31210/)をダウンロードしてインストールします。必ず***Python 3.12.10***をインストールしてください。

また後ほどエンベデッド版のPythonをComfyUIのインストールフォルダに入れます。

### ComfyUI (Git)

簡単に使いたい場合は、[デスクトップ版のComfyUI](https://www.comfy.org/download)をダウンロードして、`D:\ComfyUI\`にインストールして使いましょう。

ここからはAMDの公式手順 [Use ROCm on Radeon and Ryzen](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.2/index.html#use-rocm-on-radeon-and-ryzen) に従い、Gitのリポジトリに公開されているComfyUIをインストールします。

#### [Use ROCm on Radeon and Ryzen](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.2/index.html#use-rocm-on-radeon-and-ryzen)

1. [Install PyTorch via PIP](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.1.1/docs/install/installrad/windows/install-pytorch.html#install-pytorch-via-pip) に従いPyTorchをインストールします。管理者権限でコマンドプロンプトを起動します。
    
    1. ROCm環境を設定するコマンドを入力します。
       ``` {.copy}
        pip install --no-cache-dir ^
            https://repo.radeon.com/rocm/windows/rocm-rel-7.2/rocm_sdk_core-7.2.0.dev0-py3-none-win_amd64.whl ^
            https://repo.radeon.com/rocm/windows/rocm-rel-7.2/rocm_sdk_devel-7.2.0.dev0-py3-none-win_amd64.whl ^
            https://repo.radeon.com/rocm/windows/rocm-rel-7.2/rocm_sdk_libraries_custom-7.2.0.dev0-py3-none-win_amd64.whl ^
            https://repo.radeon.com/rocm/windows/rocm-rel-7.2/rocm-7.2.0.dev0.tar.gz
       ```
    2. ROCm AMD GPUをサポートしたtorch、torchvision、torchaudioをインストールします。
       ``` {.copy}
        pip install --no-cache-dir ^
            https://repo.radeon.com/rocm/windows/rocm-rel-7.2/torch-2.9.1%2Brocmsdk20260116-cp312-cp312-win_amd64.whl ^
            https://repo.radeon.com/rocm/windows/rocm-rel-7.2/torchaudio-2.9.1%2Brocmsdk20260116-cp312-cp312-win_amd64.whl ^
            https://repo.radeon.com/rocm/windows/rocm-rel-7.2/torchvision-0.24.1%2Brocmsdk20260116-cp312-cp312-win_amd64.whl
       ```
    3. PyTorchのインストールを確認します。
        1. PyTorchのインストールを確認します。

            `python -c "import torch" 2>nul && echo Success || echo Failure` 

        2. GPUが利用可能か調べます。

            `python -c "import torch; print(torch.cuda.is_available())"`
        
        3. インストールされたGPUデバイス名を表示します。

            `python -c "import torch; print(f'device name [0]:', torch.cuda.get_device_name(0))"`

        4. 現在のPyTorch環境内でコンポーネント情報を表示します。

            `python -m torch.utils.collect_env`

2. [Install ComfyUI](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.1.1/docs/advanced/advancedrad/windows/comfyui/installcomfyui.html#install-comfyui) に従いComfyUIをインストールします。  

    1. 管理者権限でコマンドプロンプトを起動し、カレントフォルダーをインストールしたい一つ上のフォルダに移動します。
        
        `D:`
        
    3. ComfyUIをGitから取得してください。

        `git clone https://github.com/comfyanonymous/ComfyUI.git`

    4. カレントフォルダを移動します。  

        `cd \ComfyUI`  
   
    5. 以下を入力し、インストールしてください。  

        `pip install -r requirements.txt`
    
    6. ComfyUIを起動します。

        `python main.py`

    7. 起動が確認できたら、`Ctrl + C`でComfyUIを終了します。

### Stability Matrix

GUIが優秀で使いやすいため、これで学習済みモデルを一元管理するためにインストールします。

1. [Stabiolity Matrix](https://lykos.ai/downloads)をダウンロードし任意のフルダーで解凍します。
2. DドライブにSMフォルダー（任意ですが、マルチバイト文字や空白が含まれると不整合の対策に悩まされる）を作成し、解凍したStabilityMatrix.exeを入れます。
3. StabilityMatrix.exeをダブルクリックし起動します。
4. StabilityMatrix上で、ComfyUI（ComfyUI-ZLUDAじゃないほう）をインストールします。
5. `D:\SM\Data\Packages\ComfyUI\extra_model_paths.yaml`が必要なので、コピーして`D:\ComfyUI\`にペーストします。
6. StabilityMatrix上のComfyUIは必要ないのでアンインストールします。
7. extra_model_paths.yamlの内容を編集します。

   #### extra_model_paths.yaml
    ```extra_model_paths.yaml {.copy}
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

### Python 3.12.10 Windows embeddable package (64-bit)

AMDの公式の手順ではROCm7.xの実行にはvenv仮想環境を使わない何かしらの理由があるはずなので、Pythonの実行環境を保護する必要があります。したがってエンベデッド版をComfyUIのフォルダに設置します。

1. `D:\ComfyUI\python_embeded` を作成します。
2. [Python 3.12.10](https://www.python.org/downloads/release/python-31210/)から、Windows embeddable package (64-bit) を任意のフォルダにダウンロードし解凍します。
3. 解凍したフォルダの中身をすべて、`D:\ComfyUI\python_embeded` にコピーします。
4. `D:\ComfyUI\python_embeded\python312._pth` をテキストエディタで開き以下のように編集します。

    #### python312._pth
    ```python312._pth {.copy}
    python312.zip
    .
    # 下記を追記（Lib\site-packagesを認識させるため）
    Lib\site-packages
    # import site のコメントアウトを外す（重要！）
    import site
    ```

### 起動用バッチファイル

起動用のバッチファイルにエンベデッド版Pythonを読み込むために追記します。

#### start.bat

```start.bat {.copy}
@echo off
setlocal
:: システムのPythonやライブラリを無視させる
set PYTHONNOUSERSITE=1
set PYTHONPATH=
:: このアプリ専用のPythonとROCmのパスを最優先にする
set PATH=%~dp0python_embeded;%~dp0python_embeded\Scripts;%PATH%
python main.py
```

 実用例として起動時の日付で出力先フォルダに日付フォルダを作成します。
 
#### ComfyUI_Date.bat

```ComfyUI_Date.bat {.copy}
@echo off
setlocal

rem PowerShellを使って確実に yyyyMMdd を取得（ロケールに左右されません）
for /f "usebackq" %%i in (`powershell -NoProfile -Command "Get-Date -Format 'yyyyMMdd'"`) do set yyyymmdd=%%i
 
rem Get the Output path
set parentPath=F:\output
    
rem Create the folder with the name yyyymmdd
set outpath=%parentPath%\%yyyymmdd%
    
:: システムのPythonやライブラリを無視させる
set PYTHONNOUSERSITE=1
set PYTHONPATH=
:: このアプリ専用のPythonとROCmのパスを最優先にする
set PATH=%~dp0python_embeded;%~dp0python_embeded\Scripts;%PATH%
    
rem --- ROCm / PyTorch 最適化設定 ---
SET PYTORCH_HIP_ALLOC_CONF=garbage_collection_threshold:0.6
SET PYTORCH_HIP_ALLOC_CONF=expandable_segments:True
SET ROCM_ENABLE_PREFETCH=1
    
rem フォルダが存在しない場合のみ作成
if not exist "%outpath%" mkdir "%outpath%"
    
echo Target path: %outpath%
     
D:
cd D:\ComfyUI
    
python main.py --output-directory %outpath% --preview-method none --reserve-vram 0.0 --cache-lru 8 --use-pytorch-cross-attention
endlocal
```

## 4.確認
1. Stability Matrixで使いたい学習済みモデルをダウンロードしてください。
2. ComfyUIを起動して、先ほどダウンロードした学習済みモデルが表示されれば成功です。

## 5.過去の環境との比較

****条件**** SDXL学習済みモデル、1080x1528画像、42ステップ、モデルを使ったアップスケールで4倍（4000x6000）に拡大
| GPU | AI | Time (s) |
| --- | --- | --- |
| ASUS TUF Gaming Radeon RX 9070 XT OC Edition 16GB GDDR6 | ComfyUI + ROCm7.2 | 81～90 |
| ASUS TUF Gaming Radeon RX 9070 XT OC Edition 16GB GDDR6 | ComfyUI + ROCm7.1.1 | 95～100 |
| ASUS ROG STRIX Radeon RX 6750 XT OC Edition 12GB GDDR6 | ComfyUI-ZLUDA + ROCm6.x | 300～310 |

Windowsネイティブ環境で、RDNA4に最適化されたROCm7.2だと、かなり良い感じで生成できます。GeForce環境がないので比較はしたことありませんが、そこそこいけるレベルではないでしょうか。