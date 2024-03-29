---
title: c-lesson 第三回「バイナリやアセンブリから見るC言語とリンカ」を終えて全内容を終了した
description: c-lesson 第三回「バイナリやアセンブリから見るC言語とリンカ」を終えて全内容を終了してとても素晴らしかったと振り返るブログ記事。
pubDate: 2019-07-08
tags: ['programming']
---

### TL;DR
- [c-lesson](https://github.com/karino2/c-lesson) でC言語の勉強をしている
- 最終回となる第三回も終えて、ついに全部終了した
- 第三回は第二回で得た知識を活用して、オブジェクトファイルやリンカの理解を通してC言語の理解を深めることができる良コンテンツ
- 最後には JIT コンパイルの課題もあるよ！
---

過去回の感想ブログ
- [第一回の感想](https://yoheikikuta.github.io/blog/2019-04-16-clesson_first_postscript/)
- [第二回の感想](https://yoheikikuta.github.io/blog/2019-07-01-clesson_second_asm/)

最初に着手してからだいぶ時間が経ってしまったが、ついに c-lesson の第三回も終えて全内容を完了した。

例によって第三回の内容の振り返りと、全内容を改めて見直した感想を書いておきたい。
第一回と第二回の感想でも書いているように素晴らしい内容で、自分にはめちゃくちゃ勉強になったというお話です。

### 第三回の内容
commit log は [こちら](https://github.com/yoheikikuta/c-lesson/commits/casm_6_jit_ps)。

第三回のベースは、コンパイラが実施する、プリプロセッサの展開 → コンパイル → アセンブル → リンク、の大枠を理解するという内容だ。
第二回で学んだ内容を駆使しながら、コンパイラの仕事を追って実際に何が行われているかを理解できるようになっている。

まずアセンブリからC言語の関数を呼ぶということをやる。
r0に変数をセットするなどの一定度のルールに従ってラベルを作るようにすれば呼び出せることを見る。
単純なC言語の関数ではあるが、実際にどのようにアセンブリへとコンパイルされるかというのを追ってみるというのはなかなか面白かった。

この回ではC言語側とアセンブリ側を眺めて比較しつつ内部では何が行われているかを理解するようになっているが、第二回の内容のおかげで追っていくことができるのが良い。
C言語の勉強をしようと思って、C言語のコードを書き、そしてコンパイラの方もちょっと理解したいと思ってもいきなりこのような内容を理解するのは辛い。
c-lesson では第二回で必要な範囲の低レベルプログラミングに触れているので、ちゃんとついていくことができる。

こうやって self-contained な形で一つのコンテンツとして提供されているのは凄い。
著者の能力と労力が伺えるところだ。

次いでアセンブルした結果のオブジェクトファイル（シンボルとバイナリの情報が含まれているもの）の内容やリンクについて理解する。
シンボルの解決とかは第二回のラベルのアドレス解決とかでやっているのでイメージもつきやすいし、リンカ周りの情報も結構膨大そうな中から必要なものに限定されていて助かる。

勉強しようという側は、多くの場合で色んなものを一気に詳しく知りたいということはない。
ここに全部書いてあるから、といきなり理論物理学教程を提示されてもなかなか読めないものだ（そういう話なのか？）。
必要であろう内容を選定して提示してくれるのは、（著者に十分な力量があって信頼できる場合は）初学者にとって実に助かるものだ。

readelf でバイナリがどのセクションに入っているか、というところでは宣言と定義の違いなどを理解できる。
この手の内容は一回気になって調べてそれっぽく書いてあるのを読んですぐに忘れる、という類のものだったが、もう少し真面目にやることができてよかった。

理解すべきセクション（バイナリを保存する際の領域の呼び名）として、text (関数の定義)、data (初期化されるグローバル変数)、bss (初期化されないグローバル変数)、が出てきて、こういうのはちょっとややこしいね。
初期化で値を詰めておくなら実行形式でデータとして値を持っておく必要があって data セクションに入るが、一方で初期化されないものならサイズの情報だけあればよくて値を持っておく必要がないので bss セクションと区別して持つように工夫している。
実際に実行形式をロードした場合に必要なメモリが確保されるようになる。

あとは実際に色々なC言語の機能を実際にコンパイルしてアセンブリをチェックする。
アセンブリが特に意味のないコードも含んでたりして読むのに結構慣れがいるな〜という感じ。
構造体のメンバに値を詰める、とかいう単純な処理でもちょっと読むのに気合いを入れなきゃいけない、具体的には [C言語のコードは単純にこう](https://github.com/yoheikikuta/c-lesson/blob/casm_6_jit_ps/sources/casm_link/04_c_sources/pointer_array.c#L47-L55) だが、[これを実行する部分に対応するアセンブリはこう](https://github.com/yoheikikuta/c-lesson/blob/casm_6_jit_ps/sources/casm_link/04_c_sources/pointer_array.s#L197-L252) なっていたりする。

典型的だけど文字列の配列とポインタの違いとかも見てみるのは良かった。
配列だとラベルの .asciz に直接文字列を置いていてそのアドレスをレジスタに格納して使うようになっているが、ポインタだと文字列が置いてある別のラベルのアドレスを指すようになっていてそれをレジスタに格納して使っているのが分かる。
こういうのちゃんと自分で読み解いて確認するのっていいよね。

最後にスタックウォークをして別の関数のローカル変数を触ってみたりして、おまけに　PostScript の四則演算の電卓を JIT しようという内容で終了となる。
おまけと呼ぶにはかなりガッツリの内容だが、JIT までやれるとは思わなかったので興味深く取り組めた。

パースしていってアセンブルしてバイナリの配列を作って関数ポインタにキャストして実行！という感じで、これまで作ったものを再利用しつつ小さいけど本質的な内容を含んでいるものを作る、というものになっている。
こういうのって専門知識を知らないとなかなか近寄りがたいイメージがあったが、これまで学んだ内容を使いつつちょっと背伸びするくらいでできるようになっていて、よく考えられているなぁと感じた。
出来上がったもののメインは [こんな感じ](https://github.com/yoheikikuta/c-lesson/blob/casm_6_jit_ps/sources/casm_link/06_jit_ps/ps_jit.c) である。
簡単なものではあるが、C言語側から引数を渡して `funcvar = (int(*)(int, int))jit_script("3 7 add r1 sub 4 mul");` みたいなのが JIT で使えるようになって楽しい。

ということで、全ての内容を終えてついに c-lesson も終了である。
大団円。やったぜ。

### 全体を振り返って
これで全部終了したので、全体を振り返ってみる。

そもそも低レベル側の勉強をしたいとか思っていたところ、ちょうど良いんじゃないですかと言われて始めたのがきっかけだったが、期待を遥かに上回るコンテンツだった。

第一回の PostScript インタプリタの実装でレビューしてもらいつつ3,000行くらいC言語を書いて基礎力をつけ、第二回でアセンブリやバイナリといった低レベルプログラミングにも触れて下まで降りていける体力をつけ、第三回でそれらの知識をリンクさせて理解を深める、ということで実によく練られている構成だった。

第三回は読み物的な要素も結構多いけど、それでも各三回それぞれが独立したコンテンツとしてもかなりの分量・内容になっていて、凄い（小並）。

PostScript をターゲットにすることで構文解析の煩雑さを回避し、分量が膨大にならないようにしつつも隅々まで自分で理解できるように配慮されていて、アセンブリやバイナリも理解に必要な部分にフォーカスして初学者でもちゃんとついていけるようになっている。

最終的に出来上がったものは（PostScript だし）こんなの作ったぜと派手に宣伝できるものではないかもしれないが、あまりC言語を触ったことがない人がちゃんと理解したいという目的においては出色の出来ではないだろうか。
そんなに色んな情報源にあたったわけではないが、少なくとも自分にとってはとても良いコンテンツだった。

こういうのを提供できるってのは凄いよなぁ。
C言語とか古いし昔やったから分かってるよとか言う人は多いのかもしれないけど、いつだってこれから学ぶ人もいるわけで、そういう人たち向けに質も量も高い水準で練られたものを提供してくれる人がいるのは有り難い。

例えば機械学習でも、いまから学びたいという人に「大学で線形代数とか微積とか変分法とか統計物理は当然やってるので既知のものとします」と言ってそこをすっ飛ばしても、自分で必要な基礎知識を身につけていくのは簡単なことではないよなぁ（統計物理はさすがに無理があるか...）。
曲がりなりにも専門家と言うからには、もしそういう人向けにコンテンツを提供するとなったときに、現代的な観点から必要なものを取捨選択して適切なものを提供できるようになってないといけないよな。比較対象にするにはこちらは質的に異なるしちょっと分量が多すぎるが。
ちなみに提供するとは言っていない。

ちと話が脱線してしまった。
正直ちょっとやってみようというには分量が多く、何度も何度も中断してしまい最初の commit （いま見たら 20180928 だった）から全部完了するまでなんやかんや8ヶ月くらい掛かってしまったが、それでも自発的に続けて最後までやりきるくらいには学びの多い内容だった。
改めて著者にお礼を言って締めたいと思います、ありがとうございました。

### まとめ
c-lesson の全三回を完走した。

よく練られて構成されている素晴らしい内容で、ほぼ何も分からんし書けないマンだった自分にとってかなり勉強になりました。

ありがとう c-lesson！一番好きな lesson です！
