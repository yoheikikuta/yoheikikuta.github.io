---
title: ブログを Astro + GitHub Pages に乗り換えた
description: ブログの構成が jekyll-now + GitHub Pages だったが、Astro + GtiHub Pages に変更したというブログ記事。
pubDate: 2024-02-01
tags: ['programming', 'env development']
---


### TL;DR
- ブログの構成を Astro + GitHub Pages に変更した [https://github.com/yoheikikuta/yoheikikuta.github.io](https://github.com/yoheikikuta/yoheikikuta.github.io)
- これまではお手軽な jekyll-now を使っていたが、もうあまり開発されてないのと細かいところ自分で色々いじれた方がいいかと思い乗り換えた
- そもそもブログの中身を書かないと意味ないのでもうちょい書きたいねぇ
---

これまでブログを jekyll-now [https://github.com/barryclark/jekyll-now](https://github.com/barryclark/jekyll-now) + GitHub Pages で構成したが、もう開発されていなそうなのと色々細かいところで手を加えたいなと感じることがあるので勉強ついでに Astro + GitHub Pages に変更した。

GitHub repository はこれ [https://github.com/yoheikikuta/yoheikikuta.github.io](https://github.com/yoheikikuta/yoheikikuta.github.io)

### やったこと
Astro [https://github.com/withastro/astro](https://github.com/withastro/astro) の getting started ドキュメントを読んで触りつつ、example の一つにあった Blog Starter Kit [https://github.com/withastro/astro/tree/main/examples/blog](https://github.com/withastro/astro/tree/main/examples/blog) を眺めながら大体これで十分だなと思ったのでこれをベースとしつつ自分好みになるようにいじった。

ブログの中で数式をちょくちょく使っていて、これまでは MathJax を使っていたが、移行に伴って KaTeX [https://katex.org](https://katex.org/) を使うようにした。
特別不満があったわけではないが、過去の環境だとインライン数式が `$` 一個だとうまくいかなかったりしてちょっと嫌だったのを解消した。

自分のブログの用途だとホスティング先としては GitHub Pages で十二分でこれまでのブログと URL は同一のものにしたかったので、過去使っていた `yoheikikuta.github.io` repository を rename して archive して、今回作ったものを `yoheikikuta.github.io` にした。

最近は GitHub Actions で GitHub Pages のサイトを publish できるが、これも [https://github.com/withastro/action](https://github.com/withastro/action) とかがあるので流用するだけだった。
お手軽ですね。

font を気にせず作ってたら、なんかスマホで最初にアクセスした時に英数字のところに font がうまく当たらずに表示されなかったので、NotoSansJP の woff 形式の font を準備して使うようにして問題を解決した。

まだいくつか手を加えたいところもあるけど、大体は良さそうなのでこれでやっていきつつ気になったところはちょくちょく直していこう。

### まとめ
ブログの構成を Astro + GitHub Pages に変更した。  
肝心の中身を方をもうちょい書いていきたいね。
