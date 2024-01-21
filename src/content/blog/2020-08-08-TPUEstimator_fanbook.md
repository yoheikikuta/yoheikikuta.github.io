---
title: 幻？の TPUEstimator ファンブックを読んだ
description: karino2 さんからもらった TPUEstimator ファンブックを読んでみた感想のブログ記事。
pubDate: 2020-08-08
tags: ['Machine Learning']
---

### TL;DR
- karino2 さんが 4,5 部だけ刷ったという TPUEstimator ファンブックを読んだ
- 15 ページ程度の短さながら TPUEstimator に関する理解と考察が述べられていてとても良かった
- こういう深みのある技術文書が増えて欲しい（自戒を込めて）
---

TPUEstimator を使ったことがあるだろうか？
（自分を含めて）BERT の学習とかを起点にして結構触ったことがあるという人が多いのではなかろうか？

Colaboratory で無料で 8 個の TPU コアを使えるというスタンドも月までブッ飛ぶサービスによって誰でも TPU が使えるので、これで TPU 使ったことがある人は多いと思ってる（とか言いながらあまり人から話聞いたことないけど）。
そこで TensorFlow でお手軽に分散学習をするためには TPUEstimator を使うということになる。

この TPUEstimator を使うと確かにいい感じに TPU 使って分散学習ができて、自分も 2019 年頭辺りにその恩恵に預かっていたのだが、なかなかこれが難しかった。
十分には理解できてなかったのでサンプルコード等を基にして何とか使っていたみたいな状態で、当時はそれ以上の情報を集めようと思っても殆どなかった。

そんな折、karino2 さんが 2019 年 8 月に TPUEstimator ファンブックを書いてコミケで売ったけど全然売れなかったと教えてくれて、自分も欲しいと伝えていた。
ちょこちょこ会っていたはずなのに本のことを忘れてたりしてなかなか貰えてなかったが、この度ついにもらうことができたのでその感想を書くというブログエントリである。

ちなみに一年半くらい経った今ならどうなのかと思って軽く調べてみたけど、まだあんまりなさそう？
いやあさすがにこれについてはもっと情報が出てるべきと思ったのだが。
とか言って自分も何か書いてるわけではないので偉そうなこと言えないが、BERT の学習コードとか公開してるし許してやってもいいだろう（自分には甘い）。
なんか良さそうなのを知ってたら教えてください。

### TPUEstimator ファンブックとは
前置きが長くなってしまったが、この本について軽く説明しておく。

karino2 さんが TPUEstimator の内部実装や設計思想や使い方に関して解説している 15 ページほどの本で、5 冊ほどしか刷ってないらしい（なので幻とタイトルに書いた）。
コミケで売れずに余った（全然ジャンル違いのところに置いてたらしいので売れるわけない）とのことで、自分が最後の一冊（見本誌）をゲットした。

この本が短いながらも深いところまで理解した上で TPUEstimator の良し悪しを語っていて面白い。
具体的なコードの解説はないが、よく理解した上で洞察を交えて書いてあるのでなかなかに読み応えがある。

Estimator と TPUEstimator の関係性や TPU と XLA の関係性あたりの話はためになったし、FeatureColumn とかは全然分かってなかったのでほうほうって感じだった。
正直なところ自分はあまりコードレベルで理解してないので、この感じでコードレベルで解説まで書いてくれたら最高だなと思った。

最近はあまり TensorFlow も触ってないので 2 系になってこの辺の TPUEstimator とかどうなっているのかなどは追えてないが、基本的な考え方を理解する上では今でもこのファンブックは役に立つだろう。
何よりこういう技術文書は読んでて楽しい。
上っ面の話ではないし、著者の考えも語られているのでなんかこう血が通ってる感じがしていいですよね。

ウェブで公開とかされてないのでもし読みたいとなってもなかなか読める機会がないですが、万一自分に会う機会があれば言ってくれれば貸せます。

### まとめ
TPUEstimator ファンブックをもらって読んだら面白い本だった。
ほんとうはもうちょっと細かいところまで書こうと思ったのだが、敢えて少数出版の物理本として出してるので中身書きすぎるのも違うかなと思ったので、これくらいにしておく。