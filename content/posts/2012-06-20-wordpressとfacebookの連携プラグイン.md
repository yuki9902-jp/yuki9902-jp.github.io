---
title: "WordPressとFacebookの連携プラグイン"
date: 2012-06-20T03:12:55+09:00
archives: ["2012-06"]
draft: false
categories: ['BLOG HISTORY', 'COMPUTER']

---

Facebookから公式に、WordPressのプラグインが公開されました。

WordPressで投稿した記事がFacebookのTimelineに掲載されるほか、「いいね」ボタン、「シェア」、「コメント」、「ユーザー」などが反映されます。

 

インストールしたものの、アカウントの認証でエラーが出ています。

エラーを解決しようと思ったのですが、ただいま、レンタルサーバーがメンテナンス中で、.htaccessを編集できないでいます。

たぶん違うところだろうけど。

解決は明日以降かな。

 

で、

「Facebook social publishing is enabled. Link your Facebook account to your WordPress account to get full functionality, including adding new Posts to your Timeline.」

とWordpressの管理画面に出ているのですが、これをクリックするとエラー、API Error Code: 191と表示されます。

ネットで調べたらFacebookのアプリ設定で、App Domainが間違っているからとかいう書き込みをみたのですが、それはどうも違うようです。

で、App DomainやHosting URLは未入力のままじゃないとだめです。

Website with Facebook Loginの項目に自分のブログのトップURL ([http://yuki9902.com/wp/](http://yuki9902.com/wp/))を入れてやります。

それ以外の項目は未入力にしておいてください。

これでFacebook側の設定を保存します。

次にWordpressから

「Facebook social publishing is enabled. Link your Facebook account to your WordPress account to get full functionality, including adding new Posts to your Timeline.」

をクリックして、アカウントをリンクさせます。

そうすると成功したみたいです。

 

アカウントのリンクは成功しましたが、記事の投稿がうまくいきません。

「いいね」や「コメント」はうまくいくのに。

しばらく封印かな。

 

WordPressのPluginの新規追加から「Facebook」で検索すると、一番最初に表示されるわ。

特に設定ガイドと実際のFacebookのアプリ設定画面が違うから、迷うかもしれないわね。

肝心なことは何もヘルプに書かれてないしね。