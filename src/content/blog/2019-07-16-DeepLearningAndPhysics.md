---
title: 「ディープラーニングと物理学」を読んだ
description: 「ディープラーニングと物理学」を読んだ感想のブログ記事。
pubDate: 2019-07-16
tags: ['Machine Learning']
---

### TL;DR
- reference が充実している点、3,4章のブラケット記法の導入、5章のサンプリングの説明、は良かった
- 7章以降の物理への応用に関しては、お話的な内容だったりどのくらい嬉しいことなのかぱっと見で判断できないものも多かった
- 物理の言葉や例で説明されている部分も多く、物理を学んでいる（た）人がディープラーニングを学ぶときに読んでみる本、という印象
---

$$
\def\bra#1{\mathinner{\left\langle{#1}\right|}}
\def\ket#1{\mathinner{\left|{#1}\right\rangle}}
\def\braket#1#2{\mathinner{\left\langle{#1}\middle|#2\right\rangle}}
$$

理論物理の研究者が書いた「ディープラーニングと物理学」が出版されたという話を目にしたので、一通り読んでみた。

出版されたという話を目にしてからちょっとググってみた感じ、「なぜか」評判が良さそうなので気になっていた。

ここで「なぜか」と書いているのは、自分の理解では物理の人々が参戦した結果としてディープラーニングの理論的理解が飛躍的に進んだという認識はまだない（ので他の分野の人では理解できない真髄を垣間見れるとかはない）し、一方で物理的な解釈を受け入れるにはやはり物理のトレーニングをしていないと難しい（ので色んな人に広く役立つものではないだろう）、と勝手に思っていたためである。

何にせよ自分で読んでみないことには内容がよく分からないので、一通り読んでみた。
印象に残ったところを雑多な感じで書いておく。

### reference が充実している
reference が結構充実しているなと思った。
この辺はさすがに研究者という感じで、異なる分野においても色々な話題についてよく調べて、それらについてちゃんと言及しているという印象。

一例だけど、ResNet の話を持ち出すときに、skip connection の可能性により早く言及しているものとして Higyway Network の話とその表式に言及していたりする。

こういうのはそれで本の中身自体が分かりやすくなるという類のものではないけど、その気になれば読者が原典を追えるようになるし、何より著者がちゃんと調べてるのが伝わって本の信頼度が上がるので良いよね。

### ブラケット記法は便利なのでみんなも使おう
ブラケット記法を導入しているのも良い。
これは純粋に記法の話なんだけど、式の見通しがよくなることも多いので是非広まって欲しい。
物理の人は量子力学で慣れているというバイアスもあるとは思うけど、これはちょっと慣れさえすれば誰でも便利に使えるものだとは思うので。

せっかくなのでブラケット記法について少し解説しておこう。
まずブラケットってなんだよというと bracket (括弧) のことであり、ペアで使う括弧 <,> を二つに分けて $\bra{\psi}$ (bra ベクトル) や $\ket{\psi}$ (ket ベクトル) のように書くものである。
ブラケット記法は bra-ket nottation と書かれて bracket の `c` は使われてないので綴りは間違いがち。

本来的にはベクトル空間 $V$ の元となるベクトルを ket ベクトル $\ket{v}$ で書くことにして、その双対空間 $V^{\star}$ の元となるベクトルを bra ベクトル $\bra{v}$ で書くことにする、というものである。
基底に依らないとか連続の場合も同じように書けるとか色々ありがたい点があるのだが、ここではごく一部だけを切り出して説明してみる。

以降では双対空間とかは忘れてしまって、さらに実数だけを考えることにして、ベクトルと言うときには機械学習で普通にベクトルと言ったときのベクトルだと思っておくようにする。

ある次元を持った列ベクトル $\overrightarrow{v}$ を $\overrightarrow{v} = \ket{v}$ と書くことにして、行ベクトルというときの $\overrightarrow{w}^{T}$ を $\overrightarrow{w}^{T} = \bra{w}$ と書くことにする。内積は以下のように書けることになる。

$$
\begin{align} 
\sum_{i} w_i v_i = \overrightarrow{w}^{T} \overrightarrow{v} = \braket{w}{v}
\end{align}
$$

真面目に基底のことを考えてみると、正規直交基底を考えれば以下のようになる。

$$
\begin{align} 
\braket{w}{v} &= \sum_{i, j} \bra{e_i} w_i v_j \ket{e_j} = \sum_{i, j} w_i v_j \braket{e_i}{e_j} = \sum_{i, j} w_i v_j \delta_{i,j} \\
&= \sum_i w_i v_i
\end{align}
$$

ということで基底に依らないことも分かる。
基底とかなんとか小難しいこと言うな、という人はとにかく普通のベクトルを表していると思っとけばまあよい。

添字を陽に書くと busy になったりしがちで、ベクトル表記は矢印とか転置記号とかごちゃごちゃしがちだが、ブラケット記法は見た目が分かりやすい（単に慣れているだけ、という説もある）。

間に何か変換行列 $M$ が挟まる場合は以下のようになる。
一般に添字の a,i は異なる範囲を走ってよい、これは変換行列で次元が変わると言ってるだけで機械学習ではしょっちゅう遭遇するケースである。

$$
\begin{align} 
\sum_{a} \sum_{i} M_{ai} w_a v_i = \overrightarrow{w}^{T} M \overrightarrow{v} = \bra{w} M \ket{v}
\end{align}
$$

ここで、間の変換行列 M を演算子として真面目に考えておく。
まず、恒等演算子は以下のように書ける。

$$
\begin{align} 
I = \sum_i \ket{e_i} \bra{e_i}
\end{align}
$$

$\ket{e_i} \bra{e_i}$ は単位ベクトルのテンソル積 $\ket{e_i} \otimes \bra{e_i}$ である。

左もしくは右から $\bra{e_j}$ もしくは $\ket{e_j}$ を掛けてクロネッカーのデルタを処理すれば、それぞれ $\bra{e_j}$ と $\ket{e_j}$ が得られるのでこれはいいだろう。
これで $M$ を以下のように書けば、成分が $\bra{e_a} M \ket{e_i}$ (ブラとケットで挟んでいれば内積でスカラーになっている) の行列であることが分かる。
ちょっと式が見慣れないかもしれないが、これも普通の行列と思っとけばいいです、という話。

$$
\begin{align} 
M = \sum_a \sum_i \ket{e_a} \bra{e_a} M \ket{e_i} \bra{e_i} = \sum_a \sum_i \bra{e_a} M \ket{e_i} \ket{e_a} \bra{e_i}
\end{align}
$$ 

これからも分かるように $M$ はケットベクトルに作用していると見ることもできるし、ブラベクトルに作用していると見ることもできる。
この性質は、同じ演算でも、順伝播の方向に作用させて進んでいくと考えたり、逆伝播の方向に作用させて進んでいくと考えたりできるので、ディープラーニングにはなかなか適している。

$$
\begin{align} 
\bra{w} M \ket{v} = \bra{w} \left( M \ket{v} \right) = \left( \bra{w} M \right) \ket{v}
\end{align}
$$ 

これで最低限の準備は整ったので、もう少し具体的な例を考えてみる。
$\ket{x_{\alpha}} = \sum_i x_{i, \alpha} \ket{e_i}$ ただし $\alpha$ は何番目のデータかを示す index として、これで最小二乗法の計算をしていくとする。

重み行列 $W$ を掛けた $\ket{out_{\alpha}} = W \ket{x_{\alpha}}$ を出力として、これと教師データ $\ket{y_{\alpha}} = \sum_a y_{a, \alpha} \ket{e_a}$ の差分を取って全データの和を取ったものが二乗誤差である。

$$
\begin{align} 
E = \frac{1}{2} \sum_{\alpha} \braket{out_{\alpha} - y_{\alpha}}{out_{\alpha} - y_{\alpha}} = \frac{1}{2} \sum_{\alpha} (\bra{x_{\alpha}} W^T - \bra{y_{\alpha}}) (W \ket{x_{\alpha}} - \ket{y_{\alpha}}) 
\end{align}
$$

あとはこれを $W$ に関して変分を取って 0 としたもの $\delta E = 0$ を解けばよい。
グッと計算すると以下を得る。

$$
\begin{align} 
\delta E = \sum_a \bra{e_a} \sum_{j} \left( \sum_{i} \bra{e_i} W \ket{e_a} \sum_{\alpha} x_{i, \alpha} x_{j, \alpha} - \sum_{\alpha} y_{a, \alpha} x_{j, \alpha} \right) \delta W \ket{e_j} = 0
\end{align}
$$

これで重み行列の各成分が満たすべき式が導出された。
データ次元の方向も要素を並べて行列演算で計算するようにすれば、よく見る表式へと書き直すことができる。

ぶっちゃけここまででは全然便利な感じがしないし複雑なだけなのでは？と思いたくなるが、先ほども少し述べたように誤差逆伝播法とかにこの記法を適用することで見通しが良くなることが分かる。
演算子の数が増えるとき（多層になるとき）にケットベクトルに作用すると考えてもよいしブラベクトルに作用すると考えてもよいので、そこで順伝播と逆伝播を見通しよく扱うことができるのである。
この辺りが書籍で解説されている内容なので追ってみてほしい。

結構長くなってしまったので、これくらいにしておく。
冒頭で便利だからみんなも使おうと書いたが、こうして紹介してみるとまあまあ難しい感じがするな。
書籍で初めてこの記法に出会ったという人、どう感じたか興味があるので感想を聞かせてください。

### 第5章はよく整理されていて解説も良かった
サンプリングのところは 30 ページ程度の分量でありながら内容も充実しているし解説も明瞭簡潔でよく書けていると感じた。

物理でも MCMC はよく使われているので、詳細釣り合いの理論的な話とかいくつかの典型的なサンプリング手法の解説とかが洗練されていて、理解しやすかった。

マルコフ連鎖の導入として天気模型で説明して遷移行列の固有値の話（ペロン・フロベニウスの定理）をするとかも、シンプルだし肝となる部分も伝わるのでいいなと思った。

イジング模型の話は物理やってないと何だそれとはなると思うが、それを無視してもこの章はサンプリングの話をよく知らないという人が読んでためになりそうだ。

### WGAN の双対性の部分の記述は物理的で小気味好いが
WGAN の説明は物理の人が慣れ親しんでいる感じの話の展開で読んでて気持ちがいい。

輸送コストエネルギーの期待値を「内部エネルギー」だと思って、ルジャンドル変換で「ヘルムホルツの自由エネルギー」に対象を移してゼロ温度極限を取ることで Kantrovich-Rubinstein duality の話に繋げるところは、おぉ〜って感じだった。

逆に言えば、物理をやってないといきなり熱力学でもそうだよね的な話がなされて置いてけぼりではある。

> 物理で最も重要な概念であるエネルギー、すわなちハミルトニアンを学んでいれば、読み進めることができるようになっています。 

という序文から物理以外の人に役に立つような本なのかと一瞬期待するが、ここに脚注があって

> 理学部の物理学科であれば 2~3 年以上、を想定しています。

とあり、ハミルトニアンを学ぶにはつまり大学で 2~3 年学ばねばならないということ？となる。

何を以って学ぶとするかとかは意見が色々あると思うのでいいとして、少なくとも解説としては物理を結構やっていないと何が言いたいか分からない部分も少なくないと思う。
さらに言えば、解説というよりは物理における対応物はこれです、という話なので、物理をやってない人は「よく分からないけど物理をやれば機械学習が深く理解できるのか！」と勘違いしないように気をつけた方がいいかもしれない。
我々は我々が慣れている言葉で理解しているに過ぎない（もちろん色々役に立つ考え方とかはあるが、それはきっとどの分野にもあるものだろう）。

ということで、自分が勝手に物理やってない人にも役に立つ本だと期待しただけで、そうではなく物理を既にやっていてそこからディープラーニングを学びたいという人のみを対象にしている本だ、ということなのだろう。

いやいやそんなことない、物理やってないけど物理の言葉で書かれてる部分もためになったぞという人がいたら興味深いのでぜひ教えてください。

### 第II部は色んな要素があってよく分からない
物理学への応用と展開ということなのでツールとしてディープラーニングを使うという話なのだと思うが、アトラクターとかテンソルネットワークとかの話はほとんどコラム的なお話で今後の可能性に期待という感じで、一方で実際にディープラーニングを使ったものはちょろとした説明と結果が載っているという感じ。

なんか物理で関連付きそうとか試せそうというトピックをつまみ食いしました、みたいな感じがしてしまって自分としてはあまり印象が良くないのだが、どうなんだろう。

自分が分かる範囲で調べたところ、相の検出とか量子多体系を解くとかはかなり有効に使われているようだ。
物性系で複雑な対象で相を同定するとか波動関数を求めるとかはかなり難しい問題だが、論文を軽く眺めたりした感じかなり強力なようだ。
ツールとして使いましたという話ではあるが、得られた発見から理論が進むことも大いに期待できるだろうし、こういうのは良いと思う。

ても本を読むだけではとりあえず適用しましたみたいに見えるので、上述のお話的な要素を削ってこの辺の事情とか意義とかをちゃんとプロとして語ってもらいたかったなぁという感じはする。

ちなみに第12章は自分には判断できないので、詳しい人に教えてもらいたい。

ホログラフィック原理が素晴らしい発明であることはある程度知ってはいるが、ホログラフィックQCDのセットアップでバルクのメトリックを求めることが物理的にどれくらい嬉しいことなのか分からない。
逆問題として定式化して解けるのは分かるんだが。
自分が現象論寄りだからか、ハドロンのスペクトルとか QGP の shear viscosity とか言われるとまだ理解しやすいのだが、バルクのメトリックを数値的に求めたというのはどういう嬉しさがあるのだろうか。

この章はディープラーニングを使うための前準備も明らかに他の章よりも力を入れてる（とはいえついていくのは厳しい）ので目玉の章なのかと思うが、結果の部分はそれっぽいことが書いてあったり量子重力に言及するだけだったりして前準備と比べて十分になされてない感じがするのが気になる。
まあこれは論文を読めということなのだろう。

ソースコードが公開されてないのは明らかにいただけない。
`コードによる実装はライブラリ依存になるので取り扱わない` という謎の注釈があるが、PyTorch なら PyTorch に慣れてる人がすぐに試せるし、他のライブラリに再実装して試してくれる人もいるかもしれないので、公開しない理由はよく分からない。
この本に限らず物理界隈ではよくある話で、これまでそういうことがなされない文化だったというのは分かるが、せっかく機械学習の手法を導入したのにソースコードを共有するやり方は導入しないのは良くないよなぁと思う。

### まとめ
「ディープラーニングと物理学」という本を読んだ。

ブラケット記法とかサンプリングの章とかは物理やっていない人にも有用だと思うのでオススメできそう。

自分が期待したものよりは表面的で、物理を学んでいる（た）人がディープラーニングを学びたいときに読んでみる本、という感じだった。
