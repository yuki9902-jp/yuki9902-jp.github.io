---
title: "GitHub Pagesのビルドをサーバー側（Actions）に完全移行してみた"
date: 2026-03-17T17:35:00+09:00
archives: ["2026-03"]
categories: ['COMPUTER']
tags: ['HUGO','GITHUBPAGE']
---

## hugoの使い方を簡潔に出来ないか

ローカルWWWサーバーのhugoで静的なhtmlファイルを作成してGitHub Pageにアップしていたわけですが、hugo serverコマンドでローカルサーバーを起動すると、hugo.tomlで設定している本番環境のbaseurlとは違うローカルホストのアドレスが静的ページに入り込み、本番環境にゴミが入り込んでしまうことがありました。ローカルサーバーを起動した場合には、都度、publicフォルダーを綺麗にしてから、hugoコマンドでbaseurlが外向きの物になっている物を作成してから、Gitにpushする（GitPageにアップロードする）必要がありました。バッチファイルを組み合わせればさほど難しいことではないのですが、なんかスマートではありません。そこでネット上の参考になる情報は無いかと徘徊していました。

## Gitサーバー側で構築して展開すれば良いじゃない

時代は変わっていたんですね。ローカルでマークダウンファイルで記事を書いて、サーバーにアップロードしてビルドしてデプロイすれば良いというのが最近の推奨だったなんて。

## 手順

1. GitHub設定の変更
2. .github/workflows に hugo.ymlを作成
3. ルートに.gitignoreを作成
4. サブモジュールの実体化 (テーマフォルダ)
5. 記事投稿時のgitコマンドを書き直す

### 1. GitHub設定の変更

リポジトリの `Settings` -> `Pages` -> `Build and deployment` -> `Source` を 「`GitHub Actions`」 に変更します。

### 2. .github/workflowsディレクトリにhugo.ymlを作成

すでに別のワークフロー「deploy.yaml」を作っていたのでそれを削除します。

#### hugo.yml

~~~yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build
        run: hugo --gc --minify

      - name: Pagefind
        run: npx pagefind --site public

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy
        id: deployment
        uses: actions/deploy-pages@v4
~~~

### 3. ルートに.gitignoreを作成

1. 除外するディレクトリ「`public/`」を記述します。以後、`public/`に、htmlファイルを`push`しないようにします。

   #### .gitignore

    ~~~ini
    public/
    ~~~

2. ルートで変更した内容をGitに送信
  
   #### cmd.exe、もしくはPowerShell

    ~~~shell
    # 1. 管理対象から外す
    git rm -r --cached public
    # 2. .gitignoreなどの変更をすべて含める
    git add .
    # 3. コミットして強制送信（歴史を一本化する）
    git commit -m "Switch to GitHub Actions: Remove public folder"
    git push origin main --force
    ~~~

### 4. サブモジュールの実体化 (テーマフォルダ)

この作業は、Github側で使用していたテーマ「mainroad」のリポジトリを参照しに行って、サーバー側でのビルド時に、テーマの中身（CSS等）がリンク切れで取得できなくなり、手前で変更したlayouts/の中身が反映されなくなったので、外部リポジトリ参照によるビルドエラーを回避するため対策を行いました。

  cmd.exe、もしくはPowerShell

  ~~~shell
  # 1. 念のため、Gitのインデックス（登録情報）から一旦外す
  git rm -r --cached themes/mainroad
  # 2. 改めて、中身が詰まったフォルダとして追加し直す
  git add themes/mainroad
  # 3. すべての更新を挙げる
  git add .
  # 4. 変更を確定する
  git commit -m "Ensure theme files are tracked as real files"
  # 5. 強制的に送り込む
  git push origin main --force
  ~~~

### 5. 記事投稿時のgitコマンド

記事をcontent/posts フォルダに入れたら、以下のコマンドを実行します。

#### publish.bat

~~~bat
@echo off

rem 1. 記事の追加・変更をすべてステージング（準備）
git add .

rem 2. コミット（メッセージに日付を入れると管理しやすい）
set datetime=%date% %time%
git commit -m "Update blog: %datetime%"

rem 3. GitHubへ送信
git push origin main

echo ---------------------------------------
echo 更新が完了しました。GitHub Actionsを確認してください。
echo ---------------------------------------
pause
~~~

## 最後に

あくまでもローカルにある物が「正」、ネット側にある物が「副」として考えて運用しています。それは他の人とは違うと思うので、参考になるかはわかりません。そもそも最初からGitHub側でbuildしてdeployするのが一般的らしいので、はじめから作成する人はそういう記事を探してみてください。
