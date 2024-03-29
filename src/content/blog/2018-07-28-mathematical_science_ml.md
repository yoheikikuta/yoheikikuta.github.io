---
title: 数理科学「機械学習の数理」を読んだ
description: 数理科学「機械学習の数理」を読んでみた感想のブログ記事。
pubDate: 2018-07-28
tags: ['Machine Learning']
---

### TL;DR
- 数理科学201808号「機械学習の数理」を読んだので感想を書いておく
- トピックは幅広くて眺めていて面白いが、基礎となる数理というより応用例みたいな感じ
- （致し方ないことだが）頁数的に説明が省略気味なので数式を追うのは結構辛い
---

[数理科学201808号](http://www.saiensu.co.jp/?page=book_details&ISBN=4910054690880&YEAR=2018) が「機械学習の数理」特集ということで読んでみた。
電子版がなく、電車に乗らずに行ける範囲の書店で取り扱ってないのでどうやって手に入れようかなと思っていたら、 @himkt 氏が貸してくれた。
ありがとうございます。
せっかくなので読んでみた感想を残しておくが、全部を読んだわけではないので読んだ部分だけ書いておくことにしよう。

### 巻頭言
人間活動を数式で定式化するときにそれが実在そのものを表すとは考えられないので数学の対象としづらいが、学習は「データから関数を求めること」として数学の対象とできる。
これを "双対" となぞらえて、学習という面に関しては発展しているが、そもそも現在の機械学習の発展は何ができたら人間の機能と呼べるのかという問いには全然踏み込めてないという主張。

巻頭言なので格好良い感じで書いてある。
ただ当然具体的な何かが書いてあるわけではないのでこれくらいにして次に進む。

### 機械学習の数学入門
なかなか興味深いタイトルであるが、誤差関数を用いた最適化や評価以外はニューラルネットワークの簡単な説明という感じ。
これはかなり入門向けに書いてあるので、そもそも機械学習を知っている人は想定読者ではなさそう。

せっかくなので最初の回帰関数の定式化だけ書いておく。
訓練データ $\{(x_i,y_i); i=1,2,\dots,N \}$ があり、これらは同時確率分布 $p(x,y)$ からサンプルされたものとしよう。
確率分布の言葉で書けば、モデル $f$ による二乗誤差の平均値は次のようになる。

$$
\begin{align}
E(f) = \iint dx dy \ p(x,y) || y - f(x) ||^2.
\end{align}
$$

条件付き確率 $ p(x,y) = p(y \vert x)p(x) $ を用いて以下の形に書き換える。

$$
\begin{align}
E(f) = \int dx \ p(x) \left[ \int dy \ p(y|x) || y - f(x) ||^2 \right].
\end{align}
$$

この誤差平均を最小化するモデルを次のように求める。

$$
\begin{align}
\text{argmin}_{f(x)} \left[ \int dy \ p(y|x) || y - f(x) ||^2 \right] \rightarrow \bar{f}(x) = \int dy \ y p(y|x).
\end{align}
$$

これを回帰関数と呼ぶ。
以降は経験平均による近似をして、過学習の話とそれを不良設定問題と呼ぶことを説明し、次元の呪いやニューラルネットワークの基本的な話をしている。

### 機械学習と微分幾何学
独立成分分析の話から入って、勾配法のリー群における不変計量を用いた最急降下法、双対接続、Wasserstein 幾何という内容。
個人的にはこのトピックが一番面白かったが、この手の話が初見の人はついていくのが厳しそうな気がする。

まず、形式的にユークリッド空間での勾配法（式(1)）を求めるところからして計算が追えなくなりかけた。
これは経験平均で置き換えたりしないとこの形にならないんじゃないかと思って困ったりした。
同じ著者が公開している [別の資料](https://staff.aist.go.jp/s.akaho/papers/ica.pdf) はもう少し計算が詳しく書いてあって、これを見るのが良さそう。

リー群の不変計量に基づく最急降下法からは微分幾何がある程度わからないと、そもそも言葉についていけなそう。
接空間とか計量とか（双対）接続という対象にある程度慣れてないと読めないだろう、という意味。

確率分布の空間のところはなかなか興味深いことが書いてあった。
$0,1,\dots,k$ の目が出るサイコロを振って得られる頻度 $q = (n_0/n,n_1/n,\dots,n_k/n)$ を $k$ 個の独立なパラメタの成す空間 $S$ の一点として考える。
独立なパラメタが線形制約を満たす部分空間 $M \subset S$ をモデルとみなせるという話だ。
線形制約はパラメタ間にある種の関係性を持たせた部分空間を張るための条件で、そのある種の関係性がモデルの存在によって生まれているということだろうか。
モデルへの当てはめは $q$ から $M$ の射影によってなされる。

その他にも以下のような statement が出てきて、やたらとみんなが使う言葉であるテンソルとは何かを理解しようというメッセージ性を感じる（個人の感想です）。
しかし自分も一般相対論を学ばなければ触れなかったであろう内容なので、他の人はどこで学んでいるんだろうか。
> 接続は空間の曲がり具合を規定する量であるが、テンソル量ではない。双対幾何ではそれを逆に利用し、うまい座標系を取ることによって接続の値が0となるようにして平坦さを実現する。

ともかくこの性質を用いて $\pm \alpha$ 接続を双対接続として射影定理や EM 法での例などを説明。
データが成す多様体とモデルが成す多様体のそれぞれで双対となるアフィン座標系を取り、互いの多様体への射影を交互に繰り返しながら最も近い点を探すというものである。
これは話としてはそうなっていそうだが、自分はちゃんと勉強したことがない。
情報幾何を真面目にやってみる機会があったら勉強してみるとしよう。

最後に双対幾何の抱える問題を解決する候補として Wasserstein 幾何について触れている。
これはどうしたって紙面が不足している感じではあるが、デルタ関数の和で与えられる経験分布の取り扱いとマッチする（積分が和に落ちる）、ダイバージェンスと異なり距離として扱える、と簡潔に説明している。

### 機械学習と数理統計
昔ながらの汎化バウンドとして Rademacher complexity や VC dimenstion の話をした後に、深層学習におけるノンパラメトリック回帰の解析をしている。

前半のバイアスとバリアンスのトレードオフに関しては特に目新しいことはないが、VC dimension によるバウンドを一般化する Dudley 積分の話は自分は知らなかった。
考えているモデル集合の全ての元に対して、それとの二乗誤差が $\epsilon$ 以下になる関数集合を持ってきたときに、その関数集合の大きさを測るというもの。
[この本](https://www.cambridge.org/core/books/mathematical-foundations-of-infinite-dimensional-statistical-models/C9731BF27A4CDBDB297404EBF1B7820E) が紹介されていて、ノンパラを真面目に勉強したくなったら読むのが良いのかもしれない。

後半は深層学習のノンパラメトリック回帰での近似性能と汎化誤差の話。
万能性定理はいいとして、それ以降は詳しい人じゃないとついていけなくてそうなるんですね以上の感想が持てない。
[Error bounds for approximations with deep ReLU networks](https://arxiv.org/abs/1610.01145) とか [Nonparametric regression using deep neural networks with ReLU activation functio](https://arxiv.org/abs/1708.06633) を読んでみよう、という感じですかね。

### 深層学習の数理
これが一番「最近っぽい内容」だった。
最近っぽいということは機械学習歴の浅い自分にとっても馴染みがある内容ということで、知らない内容はあまりなかった。

一個だけ取り上げておこう。
[Exponential expressivity in deep neural networks through transient chaos](https://arxiv.org/abs/1606.05340) である。
重みやバイアスや学習データが独立な確率分布から生成されるとするランダム深層学習において、$l$ 層の誤差伝播の信号の減衰が相関長 $\zeta$ 用いて $e^{- \frac{l}{\zeta}}$ で書けるというものらしい。
すなわち相転移点では相関長が無限大になるので、そこでは信号が減衰せず学習もしやすいので、この近傍をパラメタ初期値にして学習をするのがよいという話らしい。
これは面白そうだ、この論文知らなかったので読んでみよう。

### それ以降
それ以降の内容も読んだのだが、書くのが大変になってきたのでまとめて少しだけ書いておく。

言語とテキストの機械学習は、ディリクレ分布と単語確率の話から、隠れマルコフモデル、それを発展させた無限木構造隠れマルコフモデル、ニューラル言語モデルという内容。
無限木構造隠れマルコフモデルは見聞きするだけで自分でちゃんと調べてみたことがない。
そう考えて [無限木構造隠れMarkovモデルによる階層的品詞の教師なし学習(pdf)](http://chasen.org/~daiti-m/paper/nl226ithmm.pdf) を眺めたが、一瞥して理解できるものではなかったので、気が向いたら読む。

交通の数理と機械学習はセルオートマトンによる交通のドライバモデリングの話。
生物多様性と統計数理は生物多様性の指数や観測されなかったものの推定量の話。
どちらも読んでだいたい理解できるように分かりやすく書かれていて良かったのだが、書くのが辛くなってきたので内容は割愛する。

### まとめ
数理科学201808号を読んだ。
結構面白かったけど、やっぱりこういうオムニバス形式のものは自分で興味を持った内容をちゃんと勉強しないと身につくものが少ない（自明）。
