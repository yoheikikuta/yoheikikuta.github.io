---
title: Large Language Diffusion Models を理解する
description: 言語モデルに拡散モデルを用いた LLaDA の論文を読んで理解をまとめるブログ記事。
pubDate: 2025-06-04
tags: ['Machine Learning']
---

### TL;DR
- Gemini Diffusion で話題になったので discrete text diffusion model である LLaDA の論文を読んだ
- continuous との対比では noise が MASK になり、MASK は離散処理なので予測後に remask をして再度予測をすることで良いトークン列を生成していくモデルになっている
- autoregressive モデルが抱える課題を解決しうるモデルでもあるので、今後の発展が楽しみ
---

2025年5月20日~21日に開催された Google I/O における大量の発表の中に、Gemini Diffusion という text diffusion model の話があった。
公式ページは [https://deepmind.google/models/gemini-diffusion/](https://deepmind.google/models/gemini-diffusion/) で、その速度や next token prediction に基づく autoregressive model が孕む問題を解決しうる手法であることで注目を集めている。

continuous text diffusion model は少し読んだことがあるが、discrete text diffusion model は全然理解していなかったので、1つ論文を取り上げて読んでみる。
いくつかざっと目を通してみて、新しめの論文で割と理解がしやすそうな Large Language Diffusion Models [https://arxiv.org/abs/2502.09992v2](https://arxiv.org/abs/2502.09992v2) を読んでみることにした。

この論文のデモは以下（[https://ml-gsai.github.io/LLaDA-demo/](https://ml-gsai.github.io/LLaDA-demo/)より引用）で、これがどのように実現されているかを理解することが目的である（このデモは remask をしてないようなのでイマイチな気がする。上に貼った Gemini Diffusion のページの例の方が分かりやすいと思う。）。

![](https://ml-gsai.github.io/LLaDA-demo/static/images/diff_normal_150ms.gif)


### autoregressive より広い枠組みで言語モデルを考える
大規模言語モデルは圧倒的に next token prediction に基づいた autoregressive モデルを用いている。
$L$ をトークン列の長さとして各トークンを $x^i$ とし、モデルを $p_{\theta}$ とすると以下のように書ける。

$$
\begin{align}
p_{\theta}(x) \;=\; p_{\theta}(x^{1}) \prod_{i=2}^{L} p_{\theta}\bigl(x^{i} \mid x^{1}, \ldots, x^{i-1}\bigr),
\end{align}
$$

これに関しては何度目にしたか分からないし効果的であることが様々な側面から実証されてきた。
もはやこれが前提という感じになっているが、そもそも言語モデルがやりたいことをより広い枠組みで考えてみると、真ではあるが不明であるデータの分布 $p_{\mathrm{data}} (\cdot)$ を最尤推定による学習でモデル $p_{\theta}$ に表現させることにある（KL divergence を最小化することと等価）。

$$
\begin{align}
\max_{\theta} \mathbb{E}_{p_{\mathrm{data}}(x)} \bigl[\log p_{\theta}(x)\bigr]
\;\Longleftrightarrow\;
\min_{\theta} \mathrm{KL}\bigl(p_{\mathrm{data}}(x)\,\|\,p_{\theta}(x)\bigr)
\end{align}
$$

autoregressive モデルは驚くべき成功を収めているが、あくまでこの実現方法の1つであり、より広い枠組みで考えれば他の実現方法も存在する。
もちろん他の実現方法は autoregressive モデルのように典型的にはスケーリング則に基づいて高い性能を発揮しないと実用の選択肢に入らないが、この論文が提案する LLaDA (Large Language Diffusion with mAsking) では promising な結果が得られている（LLaMA とか LLaVA とかになぞらえた略称なんだろう）。

autoregressive モデルはかなりうまくいっているが、課題もある。

例えば、reversal curse という現象が知られている。
The Reversal Curse: LLMs trained on "A is B" fail to learn "B is A" [https://arxiv.org/abs/2309.12288v4](https://arxiv.org/abs/2309.12288v4) で示されたように、Who is Tom
Cruise’s mother? のような問題に正解できる（正解は Mary Lee Pfeiffer）場合でも Who is Mary Lee Pfeiffer’s son? は正解できないことがあるという現象である（ちなみにこの問題を最近の LLM で試すと正解できる）。
この現象はモデルや学習の仕組みを考えれば不思議ではないが、知識としては片方からもう片方を当てられると嬉しいよねということで課題として認識されている。

他には、autoregressive モデルはその性質上、過去に出力した内容に誤りがあればそれを修正する術がないので間違いが累積されていくみたいな話もある（この話は論文には書いてない）。
個人的には、人間と一緒で途中まで間違えていてもそれを破棄してやり直せばいいのでそこまでクリティカルな課題なのかという気もするが、解決できるといいのはそうだろう。

text diffusion model はこれらの課題に対するアプローチとして有望なものと考えられている。
LaDA では前者の reversal curse に対して autoregressive モデルよりも有効であり、そのほかにも In-Context Learning や Instruction Following の観点からも優秀であるとのことである。


### ざっくりと定式化
discrete text diffusion model において、continuous の場合のノイズに対応するのが mask になる。
肝になるのは、mask されたトークンを予測した後に再度 mask する過程を挟むことで、タイムステップが進むとより適切なトークンを予測し得るということである。

discrete text diffusion model の概念図は以下のようになる。
左側が前向き過程で、トークンを MASK に置き換えていくのが continuous の場合のノイズの付加に対応している。
右側が逆向き過程で、一度に MASK されたトークンを $p_{\theta}$ で予測するが、一定確率で remask をして、タイムステップを経るごとにより他のトークンも考慮して良い予測ができるようになる。

<div align="center">
<img src="https://imgur.com/rIaGgM4.png" width="900">
</div>

これは概念的な図だが、このイメージを持てれば continuous との対応が取りやすいので理解は難しくない。
$ t \in (0,1) $ で、$ x_t $ を MASK を含むトークン列として、$ x_t $ は確率 $1-t$ で各トークンが MASK されるものとする。
このとき、モデル（mask predictor）$p_{\theta} (\cdot \mid x_t)$ は以下で学習できる。

$$
\begin{align}
\mathcal{L}(\theta) \;\triangleq\; -\,\mathbb{E}_{t,\,x_{0},\,x_{t}}\Biggl[\;\frac{1}{t}\sum_{i=1}^{L}\mathbf{1}\bigl[x_{t}^{i}=M\bigr]\;\log p_{\theta}\bigl(x_{0}^{i}\mid x_{t}\bigr)\Biggr]
\end{align}
$$

ここで、記号の定義は以下の通りである。

- $L$: トークン列の長さ
- $\mathbf{1} [\text{条件式}]$: 指示関数で、条件式が True なら 1 で False なら 0
- $x^i_t$: タイムステップ $t$ における $i \ (i = 1, \dots, L)$ 番目のトークン
- $M$: MASK トークン

まず、期待値はタイムステップ $t$ と元々のトークン列 $x_0$ とタイムステップ $t$ における一部マスクされているトークン列 $x_t$ で取っている。
タイムステップ $t$ はマスクされる割合に影響するもので、$t$ が小さいほどより MASK されるようにして、$t$ が大きくなると MASK されにくくなって最終的には MASK がなくなるようにする。
具体的には、前向き過程における MASK 適用は以下の形で実施する。

$$
\begin{align}
q_{t\mid 0}(x_{t} \mid x_{0}) \;=\; \prod_{i=1}^{L} q_{t\mid 0}\bigl(x_{t}^{i} \mid x_{0}^{i}\bigr) 
\ \ \text{where} \ \ 
q_{t\mid 0}\bigl(x_{t}^{i} \mid x_{0}^{i}\bigr)
=
\begin{cases}
1 - t, & x_{t}^{i} = x_{0}^{i}, \\[6pt]
t, & x_{t}^{i} = M.
\end{cases}
\end{align}
$$

非常にシンプルである。
損失関数に戻ると、$p_{\theta} (x_0^i | x_t)$ と指示関数の効果で MASK されたトークンから元のトークンを予測する負の対数尤度を計算していることになり、straightforward な計算である。
非自明な点は overall factor の $1/t$ であるが、これは実用的には $t$ が小さい（すなわち MASK が多い）方が予測が難しいので重みを大きくしているものと解釈できる。
理論的にはこの損失関数が $-\,\mathbb{E}_{p_{\mathrm{data}} (x_0)} [ \log p_{\theta} (x_0) ] \leq \mathcal{L}(\theta)$ を満たすという重要な性質があるようだ。
これは [https://arxiv.org/abs/2406.03736v3](https://arxiv.org/abs/2406.03736v3) などで証明されているようなので、そのうち読んでみるかもしれない。

逆向き過程においては、$0 \leq s \leq t \leq 1$ なる $s$ を導入して以下のように MASK を予測していく。

$$
\begin{align}
q_{s \mid t}(x_{s} \mid x_{t}) \;=\; \prod_{i=1}^{L} q_{s \mid t}\bigl(x_{s}^{i} \mid x_{t}^{i}\bigr)
\ \ \text{where} \ \ q_{s\mid t}\bigl(x_{s}^{i}\mid x_{t}^{i}\bigr)
=
\begin{cases}
1, & x_{t}^{i} \neq M,\; x_{s}^{i} = x_{t}^{i}, \\[6pt]
\dfrac{s}{t}, & x_{t}^{i} = M,\; x_{s}^{i} = M, \\[6pt]
\dfrac{t - s}{t}\;q_{0\mid t}\bigl(x_{s}^{i}\mid x_{t}^{i}\bigr), & x_{t}^{i} = M,\; x_{s}^{i} \neq M, \\[6pt]
0, & \text{otherwise}.
\end{cases}
\end{align}
$$

この $s$ は逆向き過程における $t$ の次のステップ（前向き過程であれば逆に前のステップ）の役割を果たしている。
1番上は MASK されていないトークンがそのまま存在する確率は1であり、これは自然である。
2番目は MASK されたトークンが MASK されたままである確率が $s/t$ であり、このようにある程度 MASK のまま残すというのは BERT の頃からやられていることである（現状 $s$ の具体系が与えられてないが、 $t = 1$ ではもちろんこの確率が $0$ になるように具体系が与えられる。）。
3番目が肝であり、MASK されたトークンがあるトークンに予測される確率として $(t-s)/t \ q_{0\mid t}\bigl(x_{s}^{i}\mid x_{t}^{i}\bigr)$ で与えられており、マスクされていないトークンを $x^{\mathrm{UM}}_t$ としたときに以下のように $t$ に依存しない形で与えられることが証明されているようだ（これも [https://arxiv.org/abs/2406.03736v3](https://arxiv.org/abs/2406.03736v3)）。

$$
q_{0\mid t}\bigl(x_{s}^{i}\mid x_{t}\bigr)
\;=\;
p_{\mathrm{data}}\bigl(x_{0}^{i}\mid x_{t}^{\mathrm{UM}}\bigr)
$$

これが言えるのであれば、実際に使う場合には $p_{\mathrm{data}}$ を再現すべく学習をした $p_{\theta}$ で代用して予測をして前向き過程を進めていけばよいと分かる。
この式だけだと一度予測されたトークンはそのままであり、序盤に予測したトークンが文脈にそぐわない場合に修正ができないが、ある確率で remask を再度予測対象にすることで、より文脈を考慮したトークン予測が実現される。
具体的にはあとで見るが、シンプルなルールで remask してもいいし、予測の信頼度が低いトークンを重点的に remask してもいいし、ここは工夫の余地がある部分である。

正確に定式化するにはもう少し道具が必要だが、ここまでが理解できれば discrete text diffusion model である LLaDA がどのように機能するかはだいたい掴める。
continuous との対比で考えると、noise が MASK になり、MASK は離散的な処理なので徐々に適用するということができないので、remask をして繰り返し予測をしていくことでより良いトークン列を生成していくものになる。
BERT のように MASK されたトークンを含めて一度にモデルの予測を適用できるので、autoregressive 的な処理とは異なり逐次的にトークンを出力していく必要はない。
ただし、モデルの性質上出力するトークン列の長さ $L$ はハイパーパラメタとして設定しておく必要がある。
これは $L$ を長く取った上で EOS トークンも学習・予測対象とすることで動的な長さの出力をするようにしている。

論文では以下のように、事前学習・教師あり学習・サンプリング（推論時の生成）、を説明している。
事前学習は、典型的には DDPM でやられるようにタイムステップを1つサンプリングしてそれに基づいて MASK をして、BERT のように MASK されたトークンの予測をして、損失を計算して学習をする。
教師あり学習は、prompt と response を分け、response 部分だけで事前学習と同様に MASK の適用と MASK されたトークンの予測をして、損失を計算して学習をする。
サンプリング（推論時の生成）は、prompt に対して response を生成するが、先述のように一度予測をして終わりではなく、一定確率で remask をして再度予測をしていくというステップを繰り返してより良いトークン列の生成をしていく。

<div align="center">
<img src="https://imgur.com/v2tFJAW.png" width="900">
</div>


### アルゴリズム
ポイントは把握できたので、いくつかの処理のアルゴリズムの部分を見ておこう。
論文は本文の説明だけだと不明瞭なところがあるので、Appendix の記述を読む方が分かりやすい。

事前学習は以下の通りである。
事前学習時は $x_0$ の長さは $L = 4096$ で固定にしているが、可変長に対応できるように 1% は長さをランダムにサンプリングしてデータを切って padding をする。
可変長の対応への学習は教師あり学習がメインになるが、事前学習でも一定やっておくというものである。
式(7)はこのブログだと式(4)にあたり、トークン当たりの負の対数尤度に基づいて学習をする。

<div align="center">
<img src="https://imgur.com/pS64dpF.png" width="900">
</div>

教師あり学習は以下の通りである。
事前学習との違いは prompt (p) と response (r) に分かれていて response 部分で学習をすることで、$L'$ は response のトークン列の長さである。
教師あり学習では個々のデータの長さがまちまちになるが、EOS トークンを使って終端を明示して残りは padding することで学習に使うトークン列の長さは揃えている。
あまりちゃんと読んでなくてやや自信がないが、padding のトークンにも EOS を使い、これは推論時には削除するという処理にしているっぽい。

<div align="center">
<img src="https://imgur.com/4FViIAz.png" width="900">
</div>

サンプリング（推論時の生成）は以下の通りである。
タイムステップ数を $N$ として、$t$ は $1, 1 - \frac{1}{N}, \dots, \frac{1}{N}$ と小さくしていく。
$t$ の1つ後のステップ $s$ は $s = t - \frac{1}{N}$ として、最後のタイムステップでは MASK が全て取れるように設計されている。
具体的には12行目で次のステップ $s$ で MASK しないトークン数 $n_{un}$ を設定しているが、これが $s = 0$ で $L$ になる。
13~17行目が remask 処理で、予測確率が低い $L - n_{un}$個のトークンが再度 MASK されるようになり、予測確率は文脈に依存するので文脈に応じて変化してより良い生成になっていくと期待できる。

<div align="center">
<img src="https://imgur.com/4KmuI0e.png" width="900">
</div>

その他にも semi-autoregressive remasking と呼んでいる、出力をいくつかのブロックに分けて前のブロックの方からサンプリング処理をしていくという手法も提案されている。
これはまあできるだろうし性能を出すためのチューニングとしてはあり得るだろうなという感じ。


### 実験結果
モデル構造は BERT のような bidirectional Transformer で、モデルも [https://huggingface.co/GSAI-ML](https://huggingface.co/GSAI-ML) で公開されている。
公式実装による評価スクリプトではサンプリングのステップ数は 1024 を使っている [https://github.com/ML-GSAI/LLaDA/blob/f51cb17/eval_llada.py#L32-L48](https://github.com/ML-GSAI/LLaDA/blob/f51cb17/eval_llada.py#L32-L48)。

8B のモデルで各種タスクの検証を zero/few shot でしていて、以下で示すように LLaMA 8B と比べて全体的に上回っており、特に数学タスクは強い。
ただしこれにはモデル構造として特別な理由があるというよりは、データの品質とか分布の違いだろうと書かれている。

<div align="center">
<img src="https://imgur.com/gl992E5.png" width="500">
</div>

スケーラビリティも検証していて、autoregressive モデルと比べて遜色ないものになっており、事前学習の演算量に対してタスク性能が向上するスケーリング則は成り立っているものと考えられる。
$10^{23}$ FLOPs は GPT-3 とか Chinchilla 論文の $1/10$ 程度の演算量であり、さらに大規模化して検証するのはきっとどこかでやられているだろう。

<div align="center">
<img src="https://imgur.com/vkhtVFs.png" width="800">
</div>

また、reversal curse に関しては中国語の詩の対句ペアのデータで、詩の1行が与えられたときに順方向と逆方向をそれぞれ生成して正答率を調べており、GPT-4o (2024-08-06) が順方向 82.7, 逆方向 34.3 という正答率に対して、LLaDA 8B は順方向 48.8、逆方向 42.4 と逆方向でも高い性能を発揮することが示されている。

Instruction Following についても良さそうということで例が載っていたりするが、例を挙げてほら良さそうでしょ？という感じなので今のところなんとも言えないか。
強化学習は取り入れてなくてそれは future work ということなので、discrete text diffusion model が広く使われるようになったらその辺の感触は確かめてみたいところである。


### なぜ速いのか？
Gemini diffusion はその速度で話題になっていたが、拡散モデルは何度も繰り返してステップを進めていくものなので、その意味では速度が遅い手法である（論文でも速度に関しては特に言及されていない）。
しかしながら、推論時に全トークンをまとめて一気に処理できるので、autoregressive モデルのようにトークンを逐次的に生成していく必要がないので、その意味では速度を稼ぎやすい。
昨今では長いトークン列を生成することが多いので、そういう場合には拡散モデルの繰り返しのステップで時間が掛かる部分よりも、全トークンをまとめて処理できる利点が上回って高速な生成が実現できることになるだろう。
また、（離散の場合はあまり知らないが）拡散モデルにおいて生成を高速化する手法は様々に存在するので、それらを活用することも方向性の一つだろう。

色々なモデルが出てくるのは楽しいことなので、今後の発展を楽しみにしたい。
