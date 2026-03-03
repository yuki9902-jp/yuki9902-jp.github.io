---
title: "XMedia Recodeが落ちる"
date: 2020-09-03T23:34:17+09:00
archives: ["2020-09"]
original_url: https://ameblo.jp/yuki9902/entry-12622334835.html
categories: ['COMPUTER']
---

注）最新版の3.5.2.3にアップデートしたら落ちなくなりました。（2020/12/04）

GPUにNVIDIA GeForce GTX 1060 6GBを使っていたときは、コーデックのH.264を使ってMP4形式のファイルを作成しても、XMdeia Recodeが落ちることはありませんでした。

GPUをAMD Radeon RX 5700 XTに換えたら、XMedia RecodeでMP4形式のファイルを作成しようとするとアプリが落ちます。

Windowsのアプリケーションログを見ると、XMedia Recodeに入っているH264.dllが障害を起こして、Application errorでアプリが終了してしまっています。

ファイルコンテナーをMKV(Matroska)にして、H.264コーデックをAMF H.264エンコーダーを使うようにすると落ちません。

ファイル形式がMP4の場合、H264.dllがハードウェアの判定をせずに、AMDのドライバーには実装されていないモノを使おうとしているのでしょう。

MKVでは、BlackMagic DaVinci Resolve 16に読み込めないので、別の形式を使うことにします。

変換したいファイルがAVIコンテナーで映像はMotionJpeg形式、音声はPCMなので、これもDaVinci Resolveでは読み込めません。

mov形式のMotion Jpegは読み込めるので、XMedia RecodeでAVIからmovに変換することにしました。

この場合、Motion JpegもPCMもデコードしてからエンコードする必要は無く、どちらもコピーすることになります。

実質、ファイルのコンテナーの情報を書き換えるだけになるので、処理は一瞬で終わります。

ということで、mp4形式に変換するときにXMedia Recodeが落ちる場合はNVIDIAのGPUに載せ替えるか、XMedia Recodeを諦めてffmpegを使いましょう。