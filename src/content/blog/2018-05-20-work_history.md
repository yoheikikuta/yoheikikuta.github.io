---
title: 機械学習案件に携わってきてどんな理論的トピックを扱ってきたか 
description: 実際の仕事で機械学習案件に携わった経験を振り返ってどんな理論的トピックを扱ってきたをまとめたブログ記事。
pubDate: 2018-05-20
tags: ['Machine Learning']
---

### TL;DR
- 機械学習を仕事で使う人はどんな理論的内容を扱っているのか
- コードは GitHub にあるし研究は論文になるが、実業務で必要な理論的トピックに関してはなかなか目にする機会がない
- 自分がこれまでどんなことをしてきたのかを簡単にまとめてみた
---

以前 [機械学習をやる上で線形代数のどのような知識が必要になるのか](https://yoheikikuta.github.io/blog/2018-04-14-linear_algebra/) という記事を書いた。
これに関して知人と話している時に「ある程度知っている人がこれだけやれば十分みたいな話をするのは不適切じゃないか」という感じの話をした。
何が不適切かというのは色々な解釈がある。
ここでは、ある対象に関してそれなりに知っている人が考える「これで十分」というのは、暗黙の前提や関連事項の理解があったりして、表面に出てくるのはほんの一部を聞いてもそこまで役に立たない、という点を挙げておく。

これは結構広く成り立つことだろう。
まあそれ自体はそれでいいし、表面に出てくるものを深く知ろうと思ったら自然とそれに必要な土台の部分まで進んでいくものだと思う。

ただそう考えた時にこの手の議論はそんなに意味のある結論を導くものじゃないなぁという気もする。
色んな人々の共通部分を抜き出そうとして、結局誰にとってもまあそうかなという程度の結論になる（か、背景が共有されないまま自分はこう思うみたいな話がなされて噛み合わない）。

そういうのじゃなくて、もうちょっと自分が読んだとして面白いと思えるような話がいいよな。
それが何かなと考えたら、「その人がどんな仕事をしていてそこで実際にどんな理論的トピックを扱っているか」とか聞きたいなと思い至った。
エンジニアリングの話は GitHub で公開しているのを見れることが多いし、研究なら論文を読めばいい。
そうじゃなくて業務で機械学習案件に携わってきた時に扱ってきた理論的な話ってどんなものなのか共有する、こういうのはそんなにみたことがない（けど人のを聞いてみたいという興味がある）。

せっかくなので社会人5年目に突入したこのタイミングで自分の話を少しまとめてみよう。

### 前提の話
- 自分のバックグラウンド
  - 素粒子理論で博士号取得。
  - 社会人になった時点での機械学習に関する知識はほぼなし。
- 社会人になって実際の業務で関わった案件とそれを遂行するのにどんな理論的なトピックを扱ったかを書く
  - ほぼ0から始めたのでせっかくなのである程度時系列順に書いてみる。
  - 必ずしも業務で使ったものでなく勉強したものも書いた。自分の興味を書くという意味でまあいいっしょ。
  - 抜け漏れは多分たくさんある（まあこれはしゃあない）。
  - エンジニアリングの話（これもほぼ0から始めたので色々勉強したが、主題じゃない）等は割愛。

### 実際にやってきたことを振り返ってみる
記憶がおぼろげでもしかしたら年次が間違ってるものもあるかもしれないが、各年毎に書いてみる。

ちなみに自分は仕事でデータ分析とか機械学習をメインでやってきている。
他の内容、例えば二ヶ月間コンサルの研修に行くとか、もいろいろやってきてはいるんだが、まあ基本的にはずっと機械学習っぽいことをしてきている人間である。

#### 1年目
最初の頃は多変量解析を中心にやっていた。
業務で使ったというより OJT 的な研修とかを含めて勉強したという感じ。
重回帰やPLS回帰、そして問題になりうる多重共線性などを理解したが、数学的には特異値分解が分かっていれば問題なく、物理でもよく扱っていたので特に苦労した部分はない。

ここで目的関数を最適化するとか正則化項をどうするとかの統計的機械学習の基礎もやった気がする。
深い学習理論とかには足を踏み入れてないので、微分使いますくらいの話。
ノルム云々という話は物理をやっていれば慣れているものなので、数学的に困ったことはほぼない。
ただ物理をやっていたときは原理原則は比較的シンプルなので、そうではなくて最適化したい対象自体が人為的なのでその辺の慣れなさというのはあったと思う。

しかしてこ比とか懐かしく思い出される。
練習問題で手計算で計算して以来、一度も使ってないです。
検定の勉強もちょっとやったけど、基本的な帰無仮説や対立仮説とかt検定など大学でやったことあるものくらいだった（余談だが物理やってたときもコルモゴロフ・スミルノフ検定とかは見たことがあった）。

SPSSなどの商用ソフトをちょっと触った。
ただしどれも本当に触ったことあるというレベルで、今後もガッツリ使うことはないんじゃないかと思う。

業務ではトピックモデルとかベイジアンネットを使った分析を結構やっていた。
PLSAを使うことが多かったのでAICとかBICを理解するためにそのへんの学習理論に手を出した（カルバックライブラーからの導出とか最尤推定の理解とか）。
ベイジアンネットを使う時はベイズ的な確率の取扱を復習したけど、これは学部でやった内容を超えるものは出会ってない。
また、これらの意味を考える上で比較対象としてのLDA（とグラフィカルモデルの基礎）とか構造方程式モデリングとかをちょっと勉強したりもした。

研究開発的な業務としてディープラーニングにも着手した。
この頃は今ほど流行っていたわけでもなく情報もそんなになかったので、人工知能学会誌の連載（のちに [深層学習](https://www.kindaikagaku.co.jp/information/kd0487.htm) が出版）を読んで勉強したのを覚えている。
「ボルツマン」マシンとか言われると親しみを覚えれるのは物理をやってた人あるあるだろう。
そしてエネルギー関数を決める指導原理が特になくて機械学習は大変だなぁとか思うわけですよ。
ここでギブスサンプリングとかが出てくるのでメトロポリスヘイスティングを勉強したり、MCMCをちょっと舐めるみたいなことをした。
統計物理とかなり近しい話であるので、そこそこ昔のホップフィールドネットワークとかを調べてみたりもしていた。
この辺りをストレスなく吸収していけるのは物理やってたおかげだと思う（物理やってなくてもそうかもしれないけど、そういう人の人生は私には想像することしかできないので）。

業務でデータ分析とか機械学習を扱うのだから基本的な内容は押さえておこうと思って読んだのが、 [データ解析のための統計モデリング入門](https://www.iwanami.co.jp/book/b257893.html) と [はじめてのパターン認識](http://www.morikita.co.jp/books/book/2235) だった。
この辺は会社の同僚と業務時間後に勉強会とかで読んでいた。
どちらの本もよく書かれていて学び始めには結構良かった。機械学習をある程度理解して業務で使っていくという観点からは、
後者の本の式展開にちゃんとついていくというくらいの基礎体力は必要だと思うんだけど、どうでしょう。

見直してみると1年目のときに勉強した内容は対外発表したりほとんどしてない。
そういう文化というか習慣はこの時の自分からは遠いものだったなぁ。

#### 2年目
クライアント先に滞在して先方からお願いされる分析をするという業務もやるようになった。
例えば時系列の分析でARIMAとかを扱った。
時系列は[経済・ファイナンスデータの計量時系列分析](http://www.asakura.co.jp/G_12.php?isbn=ISBN978-4-254-12792-8)で勉強した。
この本は読んでて結構面白くて、単位根課程ではよく使う漸近理論が使えず（平均へ回帰しない）、ブラウン運動に基づく漸近分布を使ったりするので興味深く読んでいた記憶がある。
ただし、個人的には時系列は理論はやってて楽しいけど、予測は難しすぎるのであんまり業務では使いたくない。
その他周りの人がやっていたので、状態空間モデルとかもっと基本的なカルマンフィルタとかを勉強して、その界隈の言葉で会話はできるようになった。

構造化データを使って予測モデルを作るみたいな話もいくつかやった。
Random Forest辺りを使うことが多かったように思う。
そうするとSVMはどうなんだとかそういう話が出てくるので、見聞きするものを試しつつ自分で理論的内容をキャッチアップしていくというスタイルだった。
SVMとかをやると再生核ヒルベルト空間とかレプレゼンター定理とか出てくるわけだが、前者は量子力学でヒルベルト空間が出てくるし後者も難しいことを言ってるわけではないということは少し真面目に追えば理解できる。

ここで正直に言っておくが、ヒルベルト空間とか物理やってたときは大して理解してなかった。
まあ無限次元複素ベクトル空間でそこに住んでるベクトルが波動関数ですよね、程度の浅い理解である。
理論物理をやってる人の中には深い理解をしている人がたくさんいて、自分はかなり浅い方だという自白です。
とはいえやっぱり慣れているかどうかは凄く重要で、実際にSVMを勉強するときもスムーズに理解していくことができた。

ディープラーニングでは画像分析をやるようになって、分類とか物体検出の基本的なところを学んだ。
実際に使ったのもやはり典型的な分類とか物体検出だが、モデルを活用してちゃんとサービスをリリースするというところまではできてない。
内容はあんまり系統的に勉強した記憶はなく、例えばAlexNetとかVGGみたいな有名所のモデルの論文を読んで都度理解するみたいな感じだった。
物体検出は当時勢いがあったFaster-RCNNを読み込んでいたと思う。
Region of Proposalだとか矩形回帰だとかを理解したぞというところまでいくのに何回も読み直した記憶がある。

ディープラーニングを扱うようになると多次元配列の計算をガリガリやる必要があるが、そういうのは一般相対論をやった人からすると困難はない（どの添字に関して演算をしてるのか明確に書いてなくて困るということはあった）。
そういう意味では多様体とか出てきても特に困ることはない。
とはいえ例えばシュワルツシルト計量みたいに良い性質をもつものでもないのに何をどうやって活用するのだろうと思っていたが。
実際、自然勾配法とか関連の話をある程度真面目にやる人以外で多様体がどうとか重要になった人はどれくらいいるのだろうか。
自分は純粋に論文を読む以外で必要になったことはない（あ、Poincare Embeddingとかなら実務でも遭遇しそうかな）。

また、画像を扱うようになっていわゆる一昔前の手法も理解のために勉強した。
HOGとかSIFTとかに代表される特徴量とかですね。
この辺はちょっとした分析とかディープラーニングとの比較だとかでちょこちょこ使っていた。
MATLABでやってた。

レコメンドの案件をやるようになってからはランク学習を勉強した。
pointwiseやpairwiseなどの基本的な取り扱い（listwiseは使ったことない）や、損失関数や精度指標をちゃんと理解するみたいなところから始めた。
理解のためにSVMを使った論文はいくつか読んだが、実際に自分が使うモデルとしてはGBDTを選んだ。
ここでboostingを真面目に勉強して、RandomForestやAdaBoostやGradient Boostingなどを理解した。
汎関数微分とかが出てくるわけだが、こいつは物理ではよく出てくるもので、久しぶりに出てきてくれてありがとうと思えるくらいのものだった。
ここでやったレコメンドは最終的にはちゃんとサービスインして、かつ内容を論文にしてPAKDD(long)にacceptされた。

2年目からは少しずつ論文を書いたり論文読み会で発表したりということをするようになった。
もともと自分は発表したりするのが結構好きだし、色んな意味で対外発表は自分に良い結果をもたらすようになった。
外に目を向けると自分の知らない話ばかりなので、業務に直接関係ないような話を色々勉強することも増えていたように思う。

#### 3年目
引き続きという感じ。
2年目に書いた内容の一部は3年目のものかもしれない。
転職活動を始めたということもあってか目立って新しいことに着手した記憶がない。
なぜかと思って考えていたら本を書く（そしてそのために勉強会を開催する）ということもやっていたからだった。
このときのことを考えると うっ、頭が... まあこのくらいにしておこう。

12月から転職をしてそこからはディープラーニングを使った画像分析をやることが主業務になった。
しばらくはデプロイした画像分類モデルの性能を上げるために、会社のデータを使って会社のサービスに使うモデルを作るために様々なCNNを勉強したり試したりしたという時期だった。
それまではつまみ食い的にモデルを勉強していたが、このタイミングでCNNの主たる発展を論文を読みながらちゃんと理解した。
少なくとも自分にとってはCNNのモデルの論文で数学的に難しいところはあまりない。
なのでこれらは地道に読んでいって自分の中に蓄積させていくという感じだった。

ある程度まとまって界隈の論文を読むというのは理解を進めるという意味ではやはり良いものだ。
個々の論文の内容をもう少し抽象化した概念として理解できるので、関連論文の理解のスピードは飛躍的に上がる。
例えば 1*1 convolution をいくつかの論文で目にしてその意味を考えれば、空間方向とチャンネル方向の取り扱いの理解が深まるので、depthwise とか出てきてもすんなり理解できる。

このタイミングで色々試して結果が良かったものを取り入れながらサービスを改善しつつ継続できている、というのはなかなか素晴らしいことだと思う。

goodfellowらが著者のDeep Learningを読んだのもこの年だったかな。
他社の人と closed な勉強会を開催して読んだのだった。
optimizer 辺り（よくあるSGD, momentum, RMSProp, Adam,...）は自分が発表担当であったこともあり、かなり理解を深めた。
(L-)BFGSとかこれを機会にちゃんと自分で手を動かして理解できたのは良かった（仕事で必要になる場面はほとんどないが）。

業務とはダイレクトに結びついていないが、知人を集めて closed な PRML 勉強会を開催するようにして、これはとても良かった。
ベイジアンの理解はかなり進んで、サンプリング周りとか変分推定とかはだいぶ理解が進んだ。
Bishop氏が理論物理のPh.Dであることもあってか、物理の人には読みやすい本なのでは（ただしPeskin-Schroederみたいなタイプの本が好きな人であれば）。

3年目くらいから、仕事で必要になったものそれ自体を勉強するだけというやり方からもう少し広い視点で関連付けて理解するようになった気がする。
大学院で言えば修士を修了して博士1年目ということだし、そうなっていく時期ということですねきっと。

#### 4年目
思い返してみると、社内でハッカソンを主導したり、対外発表したり、採用活動（学会スポンサー含む）したり、副業をしたり、で忙しい年だった気がする。
更に論文を書いたり学会で座長をしたり派遣プログラムでNIPSに行ったりとアカデミックな活動もそこそこやった。

業務としては機械学習をサービスに載せるには割とまだギャップがあるということを思い知ることが多かった。
opensetの問題とかカテゴリ間の類似度の問題とかに直面して、関連しそうな論文を探して読んだりした。
前者では極値理論とか出てくるので極値分布とかをちょっと調べたが、一昔前に色々やられてる内容まで立ち戻って勉強したりはしてない（ので自分で使いこなせるとかいうレベルにはない）。
後者ではそんなに調べられている前例がなかったので、自分たちで色々やってそれを論文にまで持っていった。
これが良い学会に通れば文句なしなのだが、そうは甘くなかった。
実際の業務でやった内容を論文にして良い学会に通すということができればかなり満足度が高いんだがなぁ...
今回自分たちがやったものはまだそのレベルまでいってないということでした。

機械学習を実務でやるのに面白いところとして、研究と実サービスは結構乖離しているが分断されてるわけではないというのが一つの要素として挙げられると思う。
研究には研究の目的があるのでそれをそのまま実サービスに移植できるわけではない場合が多いが、とは言え直面する技術的困難を乗り越えるために研究の内容が有用だったり自分のアイデアが研究として価値を持ったりもし得る。
この辺はかなりレベル感の違いはありそうだが、自分が取り組んでいるものはこういうものだという認識。

数学っぽい内容としてはGAN周りの理解を深めるために関数解析とかを少しやったりしたが、これはまだまだ表面的な感じ。
幾何・代数・解析としたときに解析（もうちょっと特定すると測度論とか実解析）が一番手薄だなという物理の人は多そう（個人の感想です）。

他にも色々やった気がするが、この年にやった内容のかなりの部分は発表資料があって公開してるし、こんなもんで終わらせておこう。

### まとめ
業務で機械学習案件に従事する人がどんな理論的なトピックを扱ってきたのかを知るのは面白そう。
とりあえず自分のを簡単にまとめてみた。途中から飽きて明らかに手を抜いているが、それはそういうものだ。

振り返ってみると、理論的な内容は相当部分が物理をやっていたときに勉強した土台に助けられていることが分かる。
急がば回れ、みんなで物理をやろうということですね（これは冗談です）。
