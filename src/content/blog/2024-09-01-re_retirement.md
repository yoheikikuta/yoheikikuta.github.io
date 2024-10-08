---
title: 仕事を辞めて無職になりました（5年半ぶり2回目）
description: 5年半ぶりに仕事を辞めて無職になったので決意表明をするブログ記事。
pubDate: 2024-09-01
tags: ['仕事']
---

### TL;DR
- 20240831 で Ubie 株式会社を退職して5年半ぶりに無職になりました
- 無職期間中に生成AIモデルの基礎の本を書こうと思うので出版社の知り合いがいる人は繋いでもらえると嬉しいです
- 完全無職だとキャッシュフローが厳しいので週2~3日くらいで生成AI周りの業務委託があれば誘ってもらえると嬉しいです
---

20240831 をもって退職をして無職になりました。
5年半ぶり 2 回目の無職です。
性懲りもなくまたやってしまいました。
再就職の予定は未定ですが、とりあえず今年中いっぱいくらいは自分のことや家族のことを中心に時間を使う想定です。
仕事を辞めたのは自分や家族の時間の使い方を考えた結果です。
仕事自体は充実していたし、次はこういうことをやっていきたいなども考えていたが、諸々あってプライベートな事情を優先することにしました。

プライベートな事情としては家庭のこと（家族のことなので陽には書かないが、何か困った事態が発生したとかではなくて、人生プランを踏まえた時間の使い方の話）などもあるが、大きな要素としては自分の人生でもう一冊書籍を書きたいというものがあり、このタイミングでそれに取り組むことにした。
これまではあまり具体的なプランはなくそのうち取り組むかな〜とか考えていたが、仕事の事情とか家庭の事情とかあって、今の生活の延長線上でいつかやるとか全然無理だなと感じていたので、他の要素も重なったこのタイミングで一度仕事を辞めることを意思決定した次第である。

ちなみに生成AIモデルの土台をちゃんと理解する本を書こうと思っている。

### 生成AIのモデルを理解する書籍を書こうと思うので興味ありそうな出版社をご紹介ください
本を書こうと思っている、というか既に書き始めている、が別に出版社が決まっているとかではない。
出版社から出すこと自体が目的ではなくて、自分が書きたいものをちゃんとまとめて出すのが目的なので技術書典とかでもいいのだが、企画が通るなら出版社から出したいと考えている。

どんな感じの内容にするかを簡単に紹介するので、出版社に繋いでもいいよという人がいたら [https://x.com/yohei_kikuta](https://x.com/yohei_kikuta) とか diracdiego@gmail.com に連絡くれたら嬉しいです。
繋いでもらったら出版社の方にもっと詳しく内容を説明します。

**(20240901 22:00 追記) こちら既にお声がけいただいているところもあるので、順次進めさせていただきます。並行に進めるとご迷惑をおかけする可能性があるので、最初のところで企画が通らなかったら次のところにご相談させていただくという形で進めます。**

内容に関しては、生成AIモデルの土台となっている要素をちゃんと理解する、というものを考えている。
トピックとしては、Embedding や　Tokenization、Transformers と GPT（含む in-context learning）、スケーリング則を始めとした特徴的な性質、拡散モデルと画像生成、CLIP などに代表されるマルチモーダルなモデル、生成AIモデルの評価、etc......という感じを想定している。

生成AIは進化が早いので最先端の部分を紹介しようとしてもすぐに古くなってしまうが、Transformersをはじめとして土台になっている部分を深く理解することは将来に渡り役に立ち続けると考えている。
トピックだけ見ると類書がありそうにも思えるが、自分が書く場合に特徴となりそうな点としては以下が挙げられる：

1. 生成AIモデルの土台となっている理論的要素を原論文レベルで理解する（高度な数理的解析が対象ではなくモデルの背景や構成を数式含めて理解する）
2. 他の情報源ではあまり取り扱われていない要素も取り扱う
3. 理解を深めるための問題と解答を提供する

1点目は、原論文のレベルでちゃんと理解することに重きを置く。
表面的な帰結で終わらずに原論文の考えを感じ取るのは楽しいし、自分自身の頭で原論文レベルの理解ができるようになれば、その後の発展を自力で読み解いていくことができるためである。

例としてはやや枝葉末節なきらいもあるが、例えば Attention Is All You Need 論文の Table 1 をちゃんと解説している情報源は自分が知る限りほぼない。
この表の `Self-attention` は Transformers で採用している self-attention の計算量とは異なるので注意が必要だが、殆どの場合そのことに気付いていないように見受けられる。
そういった部分にもちゃんと deep dive して、原論文で何を主張しているのかを自分自身の力で読み解けるようになることを目指す。
別にこれが理解できてないと実際に使う時に困るとかではないわけだが、一次情報をちゃんと理解することは今後自分自身の力で理解を広げていくために有用であるので、そういう他の情報源ではあまり取り扱われない部分にもアプローチしたい。

<center>
<a href="https://imgur.com/nQuFAly"><img src=https://imgur.com/nQuFAly.png width=80% title="source: imgur.com" /></a>
</center>

2点目は、気になることが多いけど他の情報源ではあまり扱われない要素についても取り扱いたい。
例えば、分布仮説は大規模言語モデルにおける非常に重要な前提であると思うが、古い論文であることもあり、ほとんどのケースで「単語の意味は周辺の単語で決まる」みたいな表現で済ませている印象である。
これも別に原論文を理解しないくても生成AIは使っていけるが、原論文のアイデアを理解することは楽しいし、ひょっとすると原論文のアイデアに触発されてそこからの発展につながるかもしれない、ということでちゃんと原論文を理解するようにする。

3点目は、理解を深めるための問題やその解答を提供したい。
これ自体は別に新しい側面はないし特別オリジナリティの高い問題を準備するとかでもないが、論文の内容をはじめとして、理解のギャップを埋めるような問題を作る。
また、解答に関しては GitHub の repository で提供して、間違いやより良い解法があれば PR で改善してもらう仕組みとかがいいよな〜と以前から思ってたのでそれをやりたい。
（全部の解答を準備しなくてもやる気のある読者がいれば解答が埋まるという嬉しい側面があるかもしれない。もちろん誰もくれないかもしれないが......）

逆に取り扱わない内容としては、生成AIモデルの実装を提供することや様々な要素を広範に紹介することである。
実装に関しては世の中にたくさん提供されているし、実装はやはり書籍よりもコードを書きながら進めていける媒体の方が進めやすいとも思うので、これは扱わないことにする。
ただし、生成AIモデルを理解するために実装を読み解く必要がある場合はコードにも踏み込む。
様々な要素を広範に紹介することに関しては、こういう話もある・ああいう話もあると言ってたくさんの参考文献を紹介することは価値があると思っているが、自分が書きたい本のコンセプトはちゃんと書籍の中でちゃんと原論文を理解するというものなので、内容は絞ってその代わり深く理解するようにすることに重きをおく。

全体的な内容として他の書籍としてけっこう趣が異なるところもあるが、もしこういう内容でも書籍化できそうという出版社があれば紹介いただきたく。
構成とかもだいたい考えているので、詳しく説明します。

### 生成AI関連で週2~3日の業務委託があればご紹介ください
完全に別のトピックですが、無職になりましたと言ったが、流石に家族がいる中で完全に無職になるのはキャッシュフローの観点で怖さもある。
ずっと無職をやるわけではないのでまあ大丈夫と言えば大丈夫だが、生成AI関連のちょうど良い業務委託案件があれば検討したいので、こちらも何かあれば紹介いただきたく。
週2~3日くらいの量で、報酬や契約期間は協議して決めたい。

こちらももし何かあれば [https://x.com/yohei_kikuta](https://x.com/yohei_kikuta) とか diracdiego@gmail.com に連絡くれたら嬉しいです。

あとフルタイムの仕事はすぐには考えてないですが、この機会に他の人がどういうことに取り組んでいるかはいろいろ話してみたいと思うので、ちょっと話そうよという人がいたら連絡ください。

全体的に他力本願感が強くて自分で読み返してちょっと笑ってしまうが、よろしくお願いします。

### 終わりに
無職の引力が強すぎてまた無職になってしまった。
どうでもいい話だが、無職になると人に話すと羨ましいとか自分も無職になりたいとか言う人が多いが、実際に無職になる人はほとんど見たことがない。
おかしい......なぜだ......自分はついついなってしまうのだが......
