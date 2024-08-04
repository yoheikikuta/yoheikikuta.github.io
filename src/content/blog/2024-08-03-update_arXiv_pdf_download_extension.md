---
title: arxiv-pdf-downloader をアップデートした
description: 過去に作った arXiv の論文の pdf を Google Drive にアップロードする Chrome 拡張をアップデートしたというブログ記事。
pubDate: 2024-08-03
tags: ['programming']
---

### TL;DR
- 過去に作った arxiv-pdf-downloader をアップデートした: [arxiv-pdf-downloader](https://github.com/yoheikikuta/arxiv-pdf-downloader)
- Manifest V3 対応やダウンロードの成否の通知を見れるようにするなどの改修をした
- 近年なかなか論文を読まない生活になっていたのでまた読んでいきたい
---

以前 [arXiv の論文を google drive に保存する Chrome extension を作った](https://yoheikikuta.github.io/blog/2018-05-04-arxiv_pdf_download_extension/) を書いたが、近年あまり論文を読まない生活だったので放置気味だった。

また読んでいきたいねと思って動かそうと思ったら諸々動かなくなっていたし、これを機会にちょっと気になるところを改修したいという気持ちもあり、手直しをしてまた使えるようにした。

repository は [https://github.com/yoheikikuta/arxiv-pdf-downloader](https://github.com/yoheikikuta/arxiv-pdf-downloader)

### 変えたところ
久々に動かそうとしたら色々壊れてたのとコードの中身については完全に忘れていることもあったので、色々確認しながらまずはとりあえず動くように直した。

その上で `chrome://extensions/` を見てたら Google Chrome 拡張機能が Manifest V2 を 2024 に deprecated にしますと表示されていたので、Manifest V3 に対応するよう変更した。参考: [https://developer.chrome.com/docs/extensions/develop/migrate](https://developer.chrome.com/docs/extensions/develop/migrate)

とは言えそんなに大きく変えているところはないのだけど、ファイルをダウンロードする際の CORS 対応のために V3 から使えるようになった宣言的にルールを指定できる API `declarative_net_request` [https://developer.chrome.com/docs/extensions/reference/api/declarativeNetRequest](https://developer.chrome.com/docs/extensions/reference/api/declarativeNetRequest) を使うようにした。
設定しているルールは以下。

```json
[
    {
        "id": 1,
        "priority": 1,
        "action": {
            "type": "modifyHeaders",
            "responseHeaders": [
                {
                    "header": "Access-Control-Allow-Origin",
                    "operation": "set",
                    "value": "*"
                }
            ]
        },
        "condition": {
            "urlFilter": "https://arxiv.org/*",
            "resourceTypes": [
                "xmlhttprequest"
            ]
        }
    }
]
```

あとは過去に自分が使っていた時に、ファイルをダウンロードした際に成否が分からない状態で Google Drive を見に行くか拡張機能の吐くログを見に行く必要があったのが不便だったので、PC 上に通知が来て成否を確認できるようにした（下記画像の右上）。

<p align="center">
  <img src="https://imgur.com/utyIndE.gif" />
</p>

無事に使えるようになったので、また頑張って論文を読んでいくことにしよう。

### macOS の notification について学んだこと
ついでに README をアップデートしてもうちょっととっつきやすくしようとして、どういう風に機能するかの gif などがあればイメージしやすいかなと思ってキャプチャを撮って gif にしようとしたのだけど、単純にキャプチャを取ろうとすると notification が出ないことを発見した。

おそらく画面収録時に notification が映り込んでしまうのを防ぐためのデフォルト設定だろうなとは思ったけどパットは解決できなかった。
公式ページ [https://support.apple.com/ja-jp/guide/mac-help/mh40583/mac](https://support.apple.com/ja-jp/guide/mac-help/mh40583/mac) を読んでいて、`ディスプレイのミラーリング中または共有中に通知を許可` というのがあって、これっぽいなと思って System Settings の Notifications で `Allow notifications when mirroring or sharing the display` をオンにした無事表示されるようになった。

### まとめ
無事にアップデートしたので、またちょくちょく論文を読んでいくことにしよう。
そもそも論として、今後も Chrome を使い続けるのかという話もあったりするが。