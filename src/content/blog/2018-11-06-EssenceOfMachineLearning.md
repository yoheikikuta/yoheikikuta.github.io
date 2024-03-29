---
title: 「機械学習のエッセンス」を読んだ
description: 機械学習のエッセンスという本を読みかなり基礎的なところから丁寧に説明してあるけどトピックはそんなにピンと来なかったなというブログ記事。
pubDate: 2018-10-06
tags: ['Machine Learning']
---

### TL;DR
- 数学や Python の基礎があやふやな人が自分で機械学習のコードを書いてみる、というのに良さそう
- とはいえ機械学習の話が始まるまでが長く（275ページ以降に現れる）、読み手のモチベーションがどこまで続くのかはよく分からない
- 機械学習以前の話が多かったり SVM が一番厚く取り上げられていたりしてトピックはいまいち同意ができなかった
---

週末に実家に帰省したとき、PC はないけど iPad Pro はあるので機械学習関連の本でも読んでみようと思い、Twitter 辺りで目にした「機械学習のエッセンス」（出版社：SBクリエイティブ）を読んでみた。
実装は全部は追ってないのだが、一通り読んだのでブログに残しておくことにする。

### 全体の感想
Python の基礎、数学的な基礎、Python による数値計算、を手厚く解説した後に 100 ページ程度いくつかの機械学習アルゴリズムの理論と実装を解説する、という流れになっている。
特徴は数学の基礎的なところを演習問題なども交えながら丁寧に解説しているという点だろうか。
機械学習を理解するということに挑戦したいが数学のハードルが高くてどこから手をつけたらいいかもわからない、という人は助かるのではないだろうか。

読む前はある程度コーディングはできるけど理論とかが追えない人向けなのかなと思ったけど、Python のかなり基礎的なところも解説している。
ターゲットは Python も理論も分からない人（つまり初学者？）ということなのだろうか？
機械学習に入る前の基礎的なところに厚くしすぎていて、肝心の機械学習に関して得られる知識が薄い感じがする。
機械学習の本というより機械学習をやるための準備運動、みたいな印象。

機械学習アルゴリズムに関してはリッジ回帰、ラッソ回帰、ロジスティック回帰、SVM、k-Means、PCA、という内容になっている。
最近のアルゴリズムの話をするわけではない（特に Deep Learning は取り扱わないと最初に明言している）のはそういうコンセプトなので別にいいとは思うけど、個人的にはもっと典型的な勾配法ベースでのアルゴリズムを厚く扱う方が現代的なアルゴリズムに進んでいく上でも有用だと思うんだけどなぁ。
2018 年に出版する本なので、2018 年だからこその視座からトピックを選んでもらいたいなと思った。
自分は SVM とか好きなので「オッ、SVM いいね」とか思うけど、この本の対象読者に SVM を理解して実装してもらうというのは苦労の割にはその後につながるものがそこまでないかなという気がする。
まあこの本で説明される SVM を理解して実装できるレベルになれば、現代的なアルゴリズムも catch up できるだろうということなのかもしれない。

### Python の話
なんでこんなに基本的な話をしているのかはちょっとよく分かってない。
この程度の内容なら前提条件とする、もしくは外部サイトを紹介して、本としては機械学習の内容を厚くした方が良いと感じる。
Jupyter Notebook の話もしているけど、以降は特に Notebook を使うことを意識したコードが登場するわけでないのもよく分からないところだ。

こういう内容が入るのは出版社の意向とか self-contained にするというモチベーションなのかと思われるけど、読者にとってどれくらい有用なんだろうか。
機械学習に興味があるけど Python を使ったことない、とかいう人に有用なのかな。
そういう人がこういう本を読んでいけるんだろうか、自分にはよく分からない。

### 数学の話
高校〜大学1,2年、くらいの特に線形代数と微積に関してかなり丁寧に解説している。
機械学習に必要になりそうな基礎をひとまとめにして提供してくれる、というのは長らく数学から離れていたような人には嬉しいのではないだろうか。
例えばラグランジュの未定乗数法とかもできるだけ平易に解説しようという意図が見れて、言葉だけ知ってたけど何だかよく分かってないという人に優しい内容になっている。

しかし、数学の話が結構長い。
しかも機械学習をやる上でなぜこれらが重要なのかは特に関係性が明らかにならず、純粋に数学としてつらつら書かれるので、頭から読んでいくのは結構辛いのではないだろうか。
機械学習パートに入ればここで学んだ内容がそのまま使われていることが分かるので、最初に機械学習パートを眺めてからの方が数学パートを頑張るモチベーションが湧くかもしれない。

とはいえ、前述の Python パートと合わせてかなりのページ数（250ページ超）が割かれているので、機械学習を知りたいけどこれらの基礎は分からないという人がどれくらい諦めずに読めるのかは興味がある。
Python とか数学とかがよく分からなくてこの本で挑戦した、という人はどういう結果になったかぜひ教えて欲しい。

### 機械学習の話
機械学習パートが全体の 1/3 以下程度、というのはなんかもったいないというか期待と違ったというか、そんな感じがする。
取り上げているアルゴリズムに関しては丁寧な解説を理論・実装の両面からしていて読者に優しいと思うけど、取り上げているアルゴリズムは 2018 年の観点ではあまり同意できるものではない。
もっと機械学習パートを増やして勾配法ベースのものを厚く取り扱った方が価値があるんだけどなぁと思うんですがどうでしょう。

自分だったら「微分可能な目的関数を設定して勾配法で最適化する」というのを一つの現代的な潮流としてそれにフォーカスすると思うけど、この本で取り上げているアルゴリズムはどういう基準で選んでいるのかな。
特に説明がなされないままいくつかが導入されるという感じで、自分には気持ちは読み取れなかった。

機械学習のエッセンス、というには機械学習の話（扱うアルゴリズムがどういうモチベーションに起因するものなのか等）が少なくて寂しい感じがする。
この本で言ってるエッセンスというのは、理解するために必要不可欠な道具としての Python とか数学、ということなのかね。

いくつかのアルゴリズムを見聞きしたり使ったことがあるけど、中身が分からんのでそれを腰を据えて理解してみたい、という人向けな感じだろうか。
数式はかなり丁寧で行間もかなり埋められているので、他の本で挑戦したけど挫折した、という人が再挑戦してみるのもいいかもしれない。

あとコードは GitHub に置いて欲しいよなぁ。
出版社のサイトからダウンロードというのは...まあこれは出版社都合なんですかねきっと。

### まとめ
「機械学習のエッセンス」という本を読んだ。
自分は特に知らない点はなかった。
数学に長く触れてないけどこれを機に機械学習の理解に挑戦したい、という人には有用かもしれない。
