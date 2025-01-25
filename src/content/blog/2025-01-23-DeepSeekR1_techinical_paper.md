---
title: DeepSeek-R1 の technical report を読んでみた
description: OpenAI o1 に匹敵する DeepSeek-R1 の technical report を読んでみたのでそのメモをまとめるブログ記事。
pubDate: 2025-01-23
tags: ['Machine Learning']
---

### TL;DR
- 数学やコーディングなど高度な reasoning タスクで OpenAI o1 に匹敵する性能を発揮した DeepSeek-R1 の technical report を読んだ
- 先行研究の手法 GRPO や他段階の学習を組み合わせて reasoning の能力が飛躍的に向上することが示された
- モデルや学習の詳細が書かれていない部分もあるが、学習済みモデルや蒸留モデルは MIT ライセンスで公開されていて凄い
---

20250120 に公開された DeepSeek-R1 は、reasoning を強化したモデルとして OpenAI o1 に匹敵する性能であり、学習済みモデルが商用利用も可能な MIT ライセンスで公開されている [https://github.com/deepseek-ai/DeepSeek-R1](https://github.com/deepseek-ai/DeepSeek-R1) ことで話題になっている。
いくつかのタスクでの性能比較が以下の図で、数学オリンピックの選抜試験などになっているアメリカの数学選抜試験 American Invitational Mathematics Examination（AIME）や競技プログラミング Codeforces では従来の DeepSeek-V3 よりも性能が大幅に向上して o1 と同等のレベルになっている。

<div align="center">
<img src="https://imgur.com/9zRJVnZ.png" width="800">
</div>

DeepSeek-R1 では technical report [https://github.com/deepseek-ai/DeepSeek-R1/blob/23807ce/DeepSeek_R1.pdf](https://github.com/deepseek-ai/DeepSeek-R1/blob/23807ce/DeepSeek_R1.pdf) も公開されているということで読んでみた。
最初は GitHub で pdf ファイルを公開するだけなのかと思ったら、20250122 には arXiv にも投稿されていた [https://arxiv.org/abs/2501.12948](https://arxiv.org/abs/2501.12948)。

technical report があるということで喜んで読んでみたが、十分に公開されているのは学習済みモデルのみであり、モデル構造（これは DeepSeek-V3-Base モデルを基にしたと書いてはあるのでそこまで新しい何かはないと思われるが）や学習の詳細やコードなどは公開されていない。
もちろんこれだけの性能のモデルを MIT ライセンスで公開している時点で驚愕ではあるが、この点は注意が必要である。
reasoning の仕組みの部分を詳しく理解したい自分にとってはやや残念ではあるが、それでもいくつかの情報は公開されているので備忘録として記事にしておく。


### 概要
OpenAI の o1 が Chain Of Thought を長くすることで reasoning （論理的思考くらいの意味で使われることが多い印象。具体的なタスクとして数学とかコーディングの問題を解く能力。）の能力が飛躍的に高まることを示した。
これは推論時に計算量を増やすことになるので、推論時のスケーリングという概念を導入したという点で興味深いが、詳細は公開されておらず公開情報で同等の性能を達成したものも存在しない。

この technical report では、まずはベースモデルがある状況で post-training として強化学習で reasoning の能力を飛躍的に向上させたモデル DeepSeek-R1-Zero を紹介し、その後に顕在化した可読性や言語混在の課題を解くための教師あり学習や multi-stage の学習を適用した DeepSeek-R1 モデルを紹介している。
また、蒸留したモデルが高い性能を発揮することも検証し、蒸留済みモデルとして (1.5B, 7B, 8B, 14B, 32B, 70B) という各種サイズのモデルも公開している。


### DeepSeekMath で提案された Group Relative Policy Optimization
強化学習のアルゴリズムとして Group Relative Policy Optimization (GRPO) という手法を用いているが、これはこの technical report が初出ではなく、同じく DeepSeek が出している DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models [https://arxiv.org/abs/2402.03300](https://arxiv.org/abs/2402.03300) で提案された手法である。

元の論文では、Proximal Policy Optimization (PPO) の課題を解決するために GRPO を導入している。
概念図は以下の通りで、PPO では Actor-Critic で Critic たる価値関数モデルを並行して学習しなければならなくてかつその学習が複雑になるという課題があり、これを解決するために価値関数モデルを用いずに既存のモデルから複数出力させてそこからベースラインを推定して価値関数モデルの代替をさせるというアイデアである。
これによって学習リソースを大幅に削減することに成功している。

<div align="center">
<img src="https://imgur.com/R99ltbS.png" width="1000">
</div>

もう少し詳しくみておく。
PPO は以下のような代理目的関数（直接的に報酬を最大化するのが困難であるため代わりに用いる目的関数）を最大化するという手法である。

$$
\begin{align}
\mathcal{J}_{\mathrm{PPO}}(\theta)
= \mathbb{E}_{q \sim P(Q), o \sim \pi_{\theta_{\mathrm{old}}}(O \mid q)}
\Biggl[
  \frac{1}{\lvert o \rvert}
  \sum_{t=1}^{\lvert o \rvert}
    \min\!\Bigl(
      \frac{\pi_{\theta}\bigl(o_t \mid q, o_{<t}\bigr)}{\pi_{\theta_{\mathrm{old}}}\bigl(o_t \mid q, o_{<t}\bigr)} \, A_t,\,
      \mathrm{clip}\!\Bigl(
        \frac{\pi_{\theta}\bigl(o_t \mid q, o_{<t}\bigr)}{\pi_{\theta_{\mathrm{old}}}\bigl(o_t \mid q, o_{<t}\bigr)},
        1-\varepsilon,\,
        1+\varepsilon
      \Bigr) A_t
    \Bigr)
\Biggr]
\end{align}
$$

登場人物が多いので整理しておくと以下の通りである。

- $\pi_{\theta_{\mathrm{old}}}$: パラメタをアップデートする前の古い policy モデル。
- $\pi_{\theta}$: パラメタ更新をする現在の policy モデル。
- $q$: 準備したデータセット $Q$ の元である question で、たとえば数学の問題のテキストなど。
- $o$: 古い policy モデル $\pi_{\theta_{\mathrm{old}}}$ によって生成された出力トークン全体で、たとえば数学の問題に対する解答など。$o_t$ は出力全体のうちの $t$ 番目のトークンである。
- $A_t$: これは advantage function で、学習した価値関数から得られる報酬 $r_{\geq t}$ を用いて計算される（ここでは詳細は論点ではないので省略）。
- $\varepsilon$: これは clip をする際に幅を決めるパラメタ。

学習におけるポイントは 2 つで、まずは clip の役割である。
これは PPO のポイントであり、少数のサンプルや局所的なノイズで過度に policy モデルが更新されて挙動が不安定になるので、シンプルで効果的な方法として更新幅を clip で制限するものである。
もう1つが GRPO による改善部分と直接的に関係してくる部分で、$A_t$ として効果的なものを設定せねばならないということである。
数学の問題で考えるならば、問題 $q$ が与えられた時に policy モデルの出力の良し悪しを決めるためには生成するテキストが正しい答えを導くものは $A_t$ が大きくなるようにしたい。
これは価値関数がうまく学習されている必要があるし、うまく学習されるといってもトークン単位だけの情報で報酬を適切に出力するのは難しいことは想像に難くない。

この $A_t$ を価値関数を使わずにうまく設定できたら効果的・効率的な学習ができると考えられ、それを提案したのが GRPO である。
question $q$ に対して $\pi_{\theta_{\mathrm{old}}}$ から $G$ 個の出力 $\{ o_1, \cdots, o_G \}$ をサンプリングし、以下の代理目的関数を設定する。

$$
\begin{align}
&\mathcal{J}_{\mathrm{GRPO}}(\theta) \notag \\
&= \mathbb{E}_{\substack{q \sim P(Q) \\ \{o_i\}_{i=1}^G \sim \pi_{\theta_{\mathrm{old}}}(O \mid q)}}
\Biggl[
  \frac{1}{G} \sum_{i=1}^{G}
    \frac{1}{|o_i|}
    \sum_{t=1}^{|o_i|}
    \min\Bigl(
      \frac{\pi_{\theta}\bigl(o_{i,t} \mid q, o_{i,<t}\bigr)}{\pi_{\theta_{\mathrm{old}}}\bigl(o_{i,t} \mid q, o_{i,<t}\bigr)}
      \,\hat{A}_{i,t},
      \,
      \mathrm{clip}\Bigl(
        \frac{\pi_{\theta}\bigl(o_{i,t} \mid q, o_{i,<t}\bigr)}{\pi_{\theta_{\mathrm{old}}}\bigl(o_{i,t} \mid q, o_{i,<t}\bigr)},
        1-\varepsilon,\,
        1+\varepsilon
      \Bigr)\hat{A}_{i,t}
    \Bigr)
  \;-\;
  \beta \, D_{\mathrm{KL}}\bigl[\pi_{\theta} \,\|\, \pi_{\mathrm{ref}}\bigr]
\Biggr]
\end{align}
$$

変更点は 2 つで、まずは代理目的関数にハイパーパラメタ $\beta$ を導入して KL divergence が組み込まれている。
これは以下の形で提案されており、正の値になることが保証されているもので、目的関数の最大化の観点では policy モデルの更新が reference モデル $\pi_{\mathrm{ref}}$ と大きく異ならないように制限する役割を担う。
元論文では教師あり学習をしてから強化学習をする流れになっていて、$\pi_{\mathrm{ref}}$ は教師あり学習をした段階のでモデルとなっている。
つまり、これから強化学習で追加でモデルを学習していくが、それが元のモデルと大きく異なりすぎないようにするという働きをする項である。
元々の PPO では reward の計算（つまり advantage function $A_t$ に関わるもの）をする際の補正として KL divergence を用いていたが、GRPO ではこれを目的関数に組み込むことで advantage function の複雑さを軽減させるという狙いがあると書かれている。
本筋とは異なるが、ここの reference で個人のWebページ [http://joschu.net/blog/kl-approx.html](http://joschu.net/blog/kl-approx.html) が参照されていて、そうなんだってなった（中身は読んでない）。

$$
\begin{align}
D_{\mathrm{KL}}\bigl[\pi_{\theta}\,\|\,\pi_{\mathrm{ref}}\bigr]
= \frac{\pi_{\mathrm{ref}}\bigl(o_{i,t}\mid q,\,o_{i,<t}\bigr)}%
       {\pi_{\theta}\bigl(o_{i,t}\mid q,\,o_{i,<t}\bigr)}
  \;-\;
  \log \frac{\pi_{\mathrm{ref}}\bigl(o_{i,t}\mid q,\,o_{i,<t}\bigr)}%
            {\pi_{\theta}\bigl(o_{i,t}\mid q,\,o_{i,<t}\bigr)}
  \;-\; 1.
\end{align}
$$

もう 1 つの変更点がメインディッシュである advantage function $\hat{A}_{i,t}$ の定義である。
元論文では outcome supervision と process supervsion の 2 つを提案しているが、数式として参照されているのは outcome supervision だけなので、こちらだけ見ておく。
outcome supervision の advantage function は policy モデルの出力 $\{ o_1, \cdots, o_G \}$ に対する報酬が $\bm{r} = \{ r_1, \cdots, r_G \}$ であるとき、以下の形で定義される。

$$
\begin{align}
\hat{A}_{i,t}
= \tilde{r}_i
= \frac{r_i - \text{mean} (\bm{r})}{\text{std} (\bm{r})}
\end{align}
$$

ここで、$\tilde{r}_i$ は出力 $o_i$ で最後のトークンで計算される正規化報酬であり、全てのトークンでこの正規化報酬を使うことになるので、最終的な答えが正しければその途中出力は良い出力だろうという考えに立脚している。
$G$ 個のサンプルの平均と分散を使って標準化をしていて、このようにグループ内の相対評価をする方法論は多くの報酬モデルでも用いられるものなので合理的であると述べられている。
pre-training （とその後の教師あり学習での fine-tuning）をした後のモデルは十分に賢いので、そのモデルの出力をサンプリングして相対的に報酬が高い出力を重視して学習すればより性能を高めることができるというのはなかなかすごいなと思う。

また、報酬の算出には報酬モデルを用いている。
将来の累積期待報酬を推定する価値関数モデルと比べれば、即時の報酬を推定するのは比較的容易であり、数学の問題を考えるのであれば今取り組んでいる問題の正しい答えが出せれば報酬を与えればよいことになり、対象とするデータによっては学習さえしなくてよいモデルも考えられる。

process supervision は MATH-SHEPHERD: VERIFY AND REINFORCE LLMS STEP-BY-STEP WITHOUT HUMAN ANNOTATIONS [https://arxiv.org/abs/2312.08935](https://arxiv.org/abs/2312.08935) という論文で提案された reasoning のステップ毎の報酬を用いるものになっているが、今回は割愛する。

これまでの道具を用いて、報酬モデルの学習も含めた iterative GRPO のアルゴリズムが提示されている。
これは reference モデルの更新の仕方を含めて DeepSeek-R1(-Zero) でもかなりの部分踏襲しているものと思われる。

<div align="center">
<img src="https://imgur.com/2jeqdou.png" width="800">
</div>


### DeepSeek-R1-Zero 
pre-training した DeepSeek-V3-Base から始めて、教師あり学習を使わずに強化学習だけで性能向上に取り組んだモデル。
先ほど紹介した GRPO を用いるが、工夫・違いとなるのは以下の点である。

- 報酬モデルの設計
  - 数学の試験問題のように正答をルールベースで評価しやすいものや、競技プログラミングのようにテストケースで正答を評価しやすいものを対象としている。
  - reasoning の出力形式に応じて評価する。具体的にはとてもシンプルで `<think></think>` というタグの間に reasoning の過程を記述するように報酬でコントロールする。
  - ニューラル報酬モデルは報酬ハックを引き起こす可能性があるということで使っていない。じゃあ何を使っているのかは書いてないが、かなりルールベースに近いシンプルなものではないかと思われる。
- reference モデル
  - DeepSeekMath では教師あり学習で fine-tuning したモデルから始めていたが、それは今の設定では存在しないので、単に pre-training したモデルから始めて iterative GRPO で更新していっていると思われる。
- 学習テンプレート
  - 以下のようなシンプルなテンプレートを使って学習をしている。可能な限りシンプルにして特定の問題解決手法を指定しないことで、強化学習によってどのように学習が進むのかを観察しやすくしていると述べている。

<div align="center">
<img src="https://imgur.com/FIdo6WC.png" width="800">
</div>

どういうデータで学習しているなどは述べられてないが、おそらく自分たちの先行研究で使ったデータセットを用いているものと思われる。
たとえば、DeepSeekMath では Common Crawl から数学の学習に適したデータを作成したりしている。

学習の結果は以下の図で、これだけでもかなり性能が上がっていることが分かるのと、強化学習のステップを繰り返すことで飛躍的に性能が向上していることが見て取れる。
ここで、 $\text{pass@}1 = \frac{1}{k} \sum_{i=1}^k p_i$ で、$p_i$ は $i$ 番目の出力が正解だったかを示すものである。
長い出力の場合に貪欲法の出力で評価をするとばらつきが大きいということで温度を非ゼロの設定（サンプリング温度が $0.6$ で top-p が $0.95$ で、$k$ はデータで変えるが $4 \sim 64$）でこのような評価をしている。
$\text{cons@}64$ は consensus の意味で $64$ 個出力を出して多数決で出力を一意に定めてそれが正解かどうかで評価をするものである。

<div align="center">
<img src="https://imgur.com/vBDzYCp.png" width="800">
</div>

これはかなりすごい結果に見える。
もちろん使っているデータなどからして数学とかコーディングを中心とした特定のタスクに特化しているモデルになっていると思うが、それでも強化学習だけでここまでの性能になることを示したというのは興味深い。
これが本当なのか？はこれだけ情報が公開されれば色々な人が検証していると思うので、近いうちに情報が出てくるものと思われる。

学習中に見られた興味深い振る舞いとして、reasoning の過程で使うトークン数が学習とともに増大していく様子が観察され、複雑な reasoning タスクを解けるようになっている。
特に、reasoning トークン数が増えていくことで、以前のステップを見直す reflection や新たな解法アプローチを試すということが外部からの指定なく発現したと述べられている。
これは非常に面白くて、十分に汎用的な知識を備えている pre-trained モデルがあれば、強化学習の枠組み（とはいえ今のセットアップだと答えが明確に分かるタイプのものを対象にしているので教師あり学習とどれだけ異なるのかという話はありそうだが）で高度な reasoning ができるようになることを示唆している。
世はまさに post-training の時代である。

<div align="center">
<img src="https://imgur.com/fg3pEiZ.png" width="800">
</div>

また、モデルがアハ体験をしたとも報告されている。
モデルが自律的に初期の回答を見直して、reasoning にかける時間を増やすようになった瞬間であると述べられている。
これはまあ確かに発見したら楽しそうではあるけど、この例を見るとアハ体験をした後に別に大したことはやってなさそうなので、単にこういう人間にとって印象深いテキストが出力されたという以上に本質的な何かは自分には感じられなかった。

<div align="center">
<img src="https://imgur.com/V1bSHDu.png" width="800">
</div>

DeepSeek-R1-Zero の課題として、出力の可読性の低下や異なる言語が混在するという点が挙げられている。
これは報酬を向上させるためには必要ではない部分なので、こういう振る舞いを見せたりするというのは予想外というものではなさそう。
これを解決するために DeepSeek-R1 を構築している。
人間にとって使いやすいモデルという意味でのチューニングが必要なのはそれはそうという感じだが、この強化学習のみの枠組みが推し進められれば人間を置いてけぼりにして LLM が勝手にどんどん進化していくという可能性もあるわけで、来るところまで来てるな〜と感じる。


### DeepSeek-R1
上述の課題を解決するために様々な変更を加える。
学習の流れは複雑になるが、簡単にまとめると以下の通りである。

- 良質な学習データを作るためのモデルを構築する
  - DeepSeek-V3-Base から強化学習に入る前に、少量の教師データを準備してそれで fine-tuning して強化学習がスムースに進められるようにする
  - 最初の強化学習ではコーディングや数学、科学、論理推論といった高度な reasoning が求められかつ報酬が明確なデータで GRPO を用いた学習をする
  - 上記の強化学習が収束したら、そのモデルのチェックポイントで reasoning タスクに対する出力をサンプリングするとともに、writing や翻訳など他のタスクのデータも準備する（80万件ほど）
- 得られた学習データを用いて DeepSeek-R1 を学習する  
  - 80万件の教師ありデータを用いて DeepSeek-V3-Base を 2 epoch fine-tuning する
  - 人間の嗜好に合わせるため、reasoning を向上させるだけでなく有用性（helpfulness）と無害性（harmlessness）も向上させる強化学習を実施する

強化学習の初期のフェーズは不安定なので、それをサポートするために少量の良質な Chain Of Thought のデータを準備して強化学習に入る前にモデルを fine-tuning する。
データの収集方法として、長い Chain Of Thought を例示とする few-shot prompt を使う、reflection や verification を実施するために明示的に指示する、DeepSeek-R1-Zero の出力で可読なものを用いる、人間のアノテーターの情報を使う、などが挙げられている。
あまり具体的には述べられていないが、これらの方法で数千件のデータを収集したとしており、これで可読性を向上させたり人間の知識を活用することで性能を向上させたりしやすいと述べられている。

最初の強化学習では、言語混在を抑えるために言語が一貫していれば与える報酬も加算して、性能は若干落ちたが可読性は増したと述べられている。
この強化学習で学習したモデルのチェックポイントを使って教師データを作成するステップでは、reasoning の prompt を準備し、rejection sampling で出力をサンプリングし、可読性の問題など質が低いものをフィルタリングで除去している。
他にもデータセットを用いて、正解データとモデル出力を DeepSeek-V3 を使って評価するという方法でも教師データを作成したと書かれており、詳細は分からないが、かなり試行錯誤してデータを作成した様子は伺える。
これで 60 万件ほどデータを作ったと述べられている。
また、高度な reasoning タスクではない writing や factQA や翻訳などのタスクも 20 万件ほど準備しており、これは DeepSeek-V3 での学習に使ったものを再利用しているとのこと。

こうして得られたデータで改めて DeepSeek-V3-Base から始めて fine-tuning をして、2 回目の強化学習として reasoning や他のタスクのデータも準備して最終的な学習をしている。
2 回目の強化学習では、reasoning タスクでは DeepSeek-R1-Zero での GRPO と同様の学習で、他のタスクでは DeepSeek-V3 でのやり方をベースとして人間の嗜好性の評価などを取り入れている。
有用性や無害性に関しては、前者は最終出力のまとめ部分だけで reasoning 過程は評価しないようにすることで reasoning 過程に影響を及ぼさないようにして、後者は reasoning 家庭も含めてリスクやバイアスや有害コンテンツ有無を評価している、とのこと。

これでようやく DeepSeek-R1 の学習が完了するが、正直 technical report の記述だけだと詳細は把握しかねる部分は多いし、自分はちゃんと読んでない DeepSeek-V3 でのやり方を踏襲している部分もあるので、表面的にこういうことをやっているという理解に留めておく。
間違いないこととして、モデルに人間にとって望ましい振る舞いをさせるためにはやはりかなり学習データには力を入れないといけないことは痛いほど理解できる。

性能は冒頭のグラフの通りで、高度な reasoning タスクで高い性能を示している。
個別のタスクの詳細な分析は載っていないが、ちょっと興味深い記述として、SWE-Bench Verified の性能は良好だが、現状ではエンジニアリング関連の強化学習がかなり限られていて、`We believe the engineering performance of DeepSeek-R1 will improve in the next version` と述べられていて、これはかなり楽しみである。


### 蒸留モデルの性能
これは結果だけ見るが、DeepSeek-R1 の出力で各種モデルを蒸留した結果が以下の表で、かなり良い性能が出ている。
technical report では、蒸留を使わずに小規模モデルに直接強化学習をしても性能が出なかったと検証されている。
小さいモデルで性能を高めるためには大きくて高性能なモデルを持っていることが重要とはよく言われるが、DeepSeek-R1 やその改善版のモデルが公開されていくことで今後も様々な優秀な軽量モデルが生まれていくと思われる。
自分はデカくて優秀なモデルにアクセスできれば十分と思っていたが、蒸留モデルでこれくらいの性能が出るとなると、自分が解きたいタスク用に tuning するとかがまた盛り上がったりするかもな〜と感じる。

<div align="center">
<img src="https://imgur.com/OcfXGAn.png" width="800">
</div>


### まとめ
詳細が書かれていない部分も多いとはいえ、情報を公開してくれるのは有り難いし、先行研究の内容も勉強になったので読んでよかった。
上手くいかなかった試みとして Process Reward Model （これは GRPO のところで割愛した process supervision のことであり、DeepSeek-R1 ではやはり outcome supervision が使われていそう） とモンテカルロ木探索（Alpha-Go とかに inspire されたとのことだが、チェスなどのゲームと比べると探索空間が膨大になって局所最適に陥りやすいなどが原因とのこと）が挙げられていて、そういうのを共有するのもいいねとなった。

自分はまだそんなに DeepSeek は評価してないけど、ちょっと触ってみると確かに性能はなかなかよさそうに見える。
面白いのは、　[https://chat.deepseek.com/](https://chat.deepseek.com/) で R1 を試すと reasoning 過程の出力を表示してくれるのでどんな内容が途中過程で出力されているかが見えることである。
自分が試した範囲だが、日本語で聞くと中国語で reasoning 過程を出力していたり、Wait, xxxxx みたいに何か考えを巡らせてるようなテキストが何度も出力されていて面白い。

個人的には総合力では OpenAI o1 の方が上に感じているし OpenAI には o3 などが控えているというのもあるしこの業界をリードしているという立場は変わらないように思うけど、reasoning で SoTA 級の性能が出ているモデルやその情報が公開されていなかった現状を打破したのは偉大だ。
ありがとう、DeepSeek。
