---
title: 参考文献の書き方についての所感
description: 主に学術文書における参考文献の書き方に関して情報を見にいきやすくするように改善したいというブログ記事。
pubDate: 2024-08-14
tags: ['Machine Learning', '雑談']
---

### TL;DR
- 参考文献の書き方は非効率的なものになっていることがある
- 現代では電子ファイルとして読むことが多いので文献の URL へのリンクは存在するなら貼って欲しい
- HTML 版がポピュラーになれば特定箇所への言及なども明確になる未来が来るかも
---

学術文書などではとくに重要性が高い参考文献だが、書き方は結構適当でもうちょっとこうしてくれれば嬉しいんだけどな〜ということがある。
特に物理・数学・計算機科学の分野において LaTeX で参考文献を扱う場合を念頭においたとき、こういうところが気に入らなくてこうして欲しいなという私見を述べてみる。

みなさんもこうした方がいいよねというご意見あれば教えてください。

### 気に入らないなと感じる時
何よりも、電子ファイル(典型的には pdf ファイル)として読むことが多いので参考文献にワンクリックでアクセスできるように文献の URL へのリンクが欲しいケースが多い。
例えば以下のような書き方はよく遭遇するが、このときどうやってこの文献の中身を調べるだろうか？

> Angelica Chen, David Dohan, and David So. Evoprompting: Language models for code-level neural architecture search. Advances in Neural Information Processing Systems, 36, 2024a.

自分の場合、タイトルをコピーしてブラウザで検索して、ヒットした [https://arxiv.org/abs/2302.14838](https://arxiv.org/abs/2302.14838) を読むことが多い。
検索をすること自体が面倒だし、NeurIPS のページを探すのはもっと面倒なので、こうなる。

もちろん昔の文献で直接的にアクセス可能な URL がない場合とかはやむなしなんだけど、昨今の論文はアクセス可能な URL を有することが多いので、自分だったら以下のように書いてくれる方が嬉しい。
これなら中身が気になるときにワンクリックで文献にアクセスして読むことができる。

> Collin Burns, Pavel Izmailov, Jan Hendrik Kirchner, Bowen Baker, Leo Gao, Leopold Aschenbrenner, Yining Chen, Adrien Ecoffet, Manas Joglekar, Jan Leike, Ilya Sutskever, and Jeff Wu. Weak-tostrong generalization: Eliciting strong capabilities with weak > supervision, 2023. URL https://arxiv.org/abs/2312.09390.

こうするとどの学会に受理された論文なのかという情報は落ちるけど、優先順位的には文献の中身を確認しやすくする方が大事だろう。
少なくとも自分はどこの学会だからどうという話よりも具体的な中身の方に興味がある。

他にも、参考文献の書き方が揃ってないのも気になる時がある。
学会や学術誌の情報が書いてあるものと arXiv の情報が書いてあるものが混在している場合、arXiv の情報のものは学会や学術誌に受理されたものではないと考えるのは自然な思考だと思うが、実際は arXiv の情報が書いてあるものが学会や学術誌に受理されているものがあるケースが多い。

具体例として、ACL 2016 に受理されている有名な論文 Neural Machine Translation of Rare Words with Subword Units は、arXiv の情報が書いてあるケースが少なくない（真面目に調べてないけど体感で半分くらい）。
これは恐らく、Google Scholar [https://scholar.google.co.jp/schhp](https://scholar.google.co.jp/schhp) でこの論文を検索して `Cite` から BibTeX の情報を取ろうとすると以下が得られるからと思う。

```bibtex
@article{sennrich2015neural,
  title={Neural machine translation of rare words with subword units},
  author={Sennrich, Rico and Haddow, Barry and Birch, Alexandra},
  journal={arXiv preprint arXiv:1508.07909},
  year={2015}
}
```

<p align="center">
  <img src="https://imgur.com/sSu27zm.png" width="80%"/>
</p>

ちなみに、`All 16 versions` から ACL 2016 の場合の BibTex 情報を取得することも可能だが、多くの人は面倒くさがってそれをやらないだろう。
Google Scholar がどういうアルゴリズムでどの BibTeX 情報を最初に表示するかは理解してないが、Google Scholar で BibTeX 情報を取得している場合は一貫性に乏しくなる可能性が高い。

### 論文を参考文献にするときは原則 arXiv にする方がよくない？
10年前はそうではなかったかもしれないが、今では機械学習関連の論文も arXiv に投稿することが普通になったので、参考文献を書くときは arXiv [https://arxiv.org/](https://arxiv.org/) で BibTeX 情報を取得して参照先を arXiv で統一する方がよくないか？と思う。

メリットは以下:
- arXiv で保存されている論文の URL へのリンクを貼ることで論文へのアクセスが容易になる
- 参照先が arXiv で統一されるので一貫性がある
- 論文のフルの情報を扱える
  - 学会や学術誌でページ数制限がある場合には情報を削ぎ落とす必要がある。典型的には証明や実験の詳細など。これらの情報が他の情報にとって重要な場合でも、論文のフルの情報を投稿できる arXiv であれば扱いやすい。
- （これは今回の観点とは独立の話だが）arXiv は複数バージョンを投稿できるので、論文の任意のバージョンを指定できる
  - 例えば最初に出した論文に間違いがあってその後修正をしてその情報が重要な場合に、修正後のバージョンを指定できる。
  - バージョン指定は [https://arxiv.org/abs/1508.07909v5](https://arxiv.org/abs/1508.07909v5) のように末尾にバージョン番号を付与すればよい。

デメリットは以下:
- arXiv に全ての論文が投稿されるわけではない。分野によって作法が違う
  - これはそう。ないものはしょうがないので arXiv に論文があるものに関しては統一する、とかが現実的にはなりそう。
  - arXiv に焦点を置いてるのは自分が興味ある分野では arXiv に論文があることが多いためで、なんにせよ参照している文献は容易にアクセスできるようにはしたいよね。
- 学会や学術誌に受理されたという情報が落ちてしまう
  - 既に述べたが、文献を参照するという意味では具体的な中身の方に興味があることの方が多いので個人的にはデメリットに感じるところはほぼない。
  - ある学術文書の信憑性を測る方法の一つとして、その学術文書が引用している文献が主要な学会の論文などをちゃんと把握しているか確かめる、というものがありうるがそういう場合ではデメリットになりそう。

個人的にはメリットの方が遥かに大きいので、そういう世界になって欲しい。
そのような方向性に向かう集団的なインセンティブは特にないので難しいとは思うが。

### 文献の特定の箇所を引用する
文献全体を引用してるけど具体的にはどこだよ！？というケースもある。
特定の定理とか式を引用する場合に、引用に際して定理とか式番号をちゃんと書いてくれればいいけど、そうでないケースも少なくないし文章であったりすると指定の仕方は難しい。

また arXiv の論文の話に限定するが、arXiv は accessibility の観点で論文の HTML 版を試験的に公開している: [https://info.arxiv.org/about/accessible_HTML.html](https://info.arxiv.org/about/accessible_HTML.html)

これが広く使われるようになれば、特定箇所だけに興味がある場合にその引用がしやすくなるので、そういう未来が来るとより引用が明確になって嬉しいかもしれない。

式の引用例: [https://arxiv.org/html/1706.03762v7#:~:text=of%20outputs%20as%3A-,Attention,(1),-The%20two%20most](https://arxiv.org/html/1706.03762v7#:~:text=of%20outputs%20as%3A-,Attention,(1),-The%20two%20most)  
文章の引用例: [https://arxiv.org/html/1706.03762v7#:~:text=matrix%20multiplication%20code.-,While%20for%20small%20values%20of,.,-3.2.2](https://arxiv.org/html/1706.03762v7#:~:text=matrix%20multiplication%20code.-,While%20for%20small%20values%20of,.,-3.2.2)
