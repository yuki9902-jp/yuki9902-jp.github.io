---
title: "TrueNAS CoreからTruNAS Communicationに移行した"
date: 2026-01-09T14:31:27+09:00
archives: ["2026-01"]
original_url: https://ameblo.jp/yuki9902/entry-12952850667.html
categories: ['COMPUTER']
tags: ['TrueNAS']
---

TrueNAS CoreとTrueNAS Scaleのエディションが廃止され、TrueNAS ScaleがCommunity EditionとEnterpriseの2つのエディションとなりました。  
  
FreeBSDがベースのTrueNAS Coreの方がWindowsからのデータ書き込みが速かった気がするんですが、もうこのエディションがなくなってしまったので、自宅のNASのOSをTrueNAS Commutnity Editonにインストールし直しました。  
  
UIは似ているんですが、設定項目の配置が違うのでそれを探すのが手間取ります。  
  
SMBのマルチチャネル接続は、チェックボックスに変わったのでこちらは簡単になりました。  
  
後はWindows側からファイルを書き込むときは、ROBOCOPYのオプションのJ、MT:2を設定することで安定した速度が確保できます。