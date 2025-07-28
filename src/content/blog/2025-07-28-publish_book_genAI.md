---
title: 2025/08/18 に技術評論社から著書「原論文から解き明かす生成AI」が発売されます
description: 執筆した書籍「原論文から解き明かす生成AI」が技術評論社から発売されることを告知するブログ記事。
pubDate: 2025-07-28
tags: ['Machine Learning']
---


### TL;DR
- 20250818 に技術評論社から著書「原論文から解き明かす生成AI」が発売されます
- 生成AIの土台となる原論文（Transformerやスケーリング則など）を詳しく読み解いて楽しむ本です
- 論文が対象なので初学者向けの本ではないですが、興味ある人はぜひ読んでみてください！ [技術評論社のページ](https://gihyo.jp/book/2025/978-4-297-15078-5)
---

執筆していた書籍が発売されるので、その告知のブログエントリです。

- 発売日: 2025/08/18
- タイトル: 原論文から解き明かす生成AI
- 出版社: 技術評論社
- 概要: 
  - 生成AIにおいて重要な土台となるモデルや現象を論文を読み解いて理解する本です。Transformer の詳細なモデル構造・テキストと画像を融合させた生成AIモデル・拡散モデルの定式化・推論時も含めたスケーリング則、などが主たる対象です。その他にも、他の書籍では扱われないが重要な土台となっている、分布仮説を実験的に支持する論文や拡散モデルの数学的基礎の論文なども取り上げています。
- 対象読者: 
  - 学部レベルの機械学習の知識があり、生成AIの基礎を理論的に理解したい人。典型的には、生成AIに関連する研究室の修士課程や博士課程に在籍する大学院生・生成AIや隣接する領域を研究している研究者・社会人で生成AIの理論的理解を必要としている人、など。
- 予約・購入はこちらから: 
  - [技術評論社のページ](https://gihyo.jp/book/2025/978-4-297-15078-5)
  - [Amazon](https://www.amazon.co.jp/o/ASIN/4297150786)
  - その他さまざまな書店やウェブサイトでも販売しています

<div align="center">
<img src="https://imgur.com/FxBj4Sm.png" width="400">
</div>

目次と簡単な内容は以下の通りです。

- 第1章 本書の読み方と論文を読み解く技術
  - 論文を読み解くことを目的としている本なので、どのように論文を取得し読み進めていくかを解説しています。
- 第2章 入力データの特徴量化
  - テキストデータの特徴量化に注目し、埋め込みや分布仮説、サブワード分割について理解を深めます。また、発展的な内容としてトークナイザーの必要性についても取り上げます。
- 第3章 生成AIモデルの大前提となる Transformer
  - Transformer の論文は生成AIを理解する上で欠かせないものなので、論文の隅から隅まで読み解きます。本書で扱う生成AIモデルは全て Transformer の構造に基づくものに限定しているので、一貫した理解が可能です。
- 第4章 Generative Pre-trained Transformerとテキスト生成
  - テキスト生成モデルとして GPT-1,2,3,4 の論文を読み解くとともに、関連する要素として In-Context Learningや Reinforcement Learning from Human Feedback なども取り上げます。
- 第5章 拡散モデルと画像生成
  - 画像生成に欠かせない拡散モデルを理解し、拡散モデルと Transformer を組み合わせた Diffusion Transformer などを解説します。
- 第6章 テキストと画像の融合
  - text-to-image モデルである unCLIP（DALL·E 2）など、入出力の組み合わせに応じていくつかのモデルを解説します。
- 第7章 生成AIモデルのスケーリング則
  - 事前学習におけるスケーリング則だけでなく、DeepSeek-V3,R1 の論文も読み解いて推論時のスケーリング則についても取り扱います。
- 第8章 生成AIモデルの評価
  - 評価の観点として、Chatbot Arena（現在は LMArena）の仕組みスコアリングの理論的枠組みや Humanity's Last Exam などの難易度の高いタスクについても紹介します。


### 本書の特徴
まず、論文を読み解くことに重きを置いている点が挙げられます。
論文は必ずしも分かりやすく書かれているものではありませんが、論文を読み解けるようになれば、新しい研究が出てきても自分で一次情報にあたれるようになるし、著者のアイデアや発見を追体験する楽しさを味わうこともできます。

本書の特徴を際立たせるためにも、生成AIの情報を幅広く整理して解説するのではなく、重要な論文に焦点を当ててそれをしっかりと理解するというスタイルの本にしました。
私自身が論文を読むことが好きでもあるので、そういう雰囲気が感じられるかもしれません。

このブログの最後に本書で扱う論文のリストを載せておきます。

内容に関しては、テキスト生成と画像生成の両方を扱っている点・推論時スケーリングも含めたスケーリング則を扱っている点・分布仮説の実験的検証など古いけど重要な基礎になっているトピックも扱っている点、などは珍しいかと思います。
生成AIに関して既にある程度の知識を有している人にとっても、読んでいて面白い内容が含まれているはずです。

また、実装に関しては本書のスコープ外としており、コードは理解を深めるために読むものが登場する程度です。
様々なトピックを扱うので実装を含めようとするとどうしても表面的になってしまったり、ページ数には制限があるのでページ数的に扱えないトピックが増えてしまったり、という理由で実装に関しては取り扱わないことにしました。

上述のような点を踏まえると、類書がないタイプの本に仕上がったのではないかと思います。
私としては色々考えてこのような形式にしましたが、その良し悪しに関してはぜひ読んで各位が判断していただきたいです。
SNS に感想を流すなども大歓迎です。


### なぜ本書を執筆したか
色々な想いはあるのですが、書き出すと大量になってしまうので、ここでは「生成AIに聞けば論文を調査したり理解したりすることが可能になってきているのに、このような本を書く意味があるか？」という疑問に対する自分なりの考えを書いておきます。

結論から述べると意味があると思います。

確かに生成AIとやりとりすることで単体の論文の理解はとてもしやすくなったし、多くの論文を調査してまとめるということもしやすくなりました。

それでも、こういう一連の論文が自分が興味のある論文であり、それをについて自分の言葉でまとめるというのは楽しい知的生産活動だし、人となりが滲み出る人間らしい営みだと感じます。
これまで積み重ねてきたものを結実させる媒体として、書籍は私にとって良い対象で、書籍執筆は総じて楽しいものでした。
仕事と家事育児をしながら執筆するのは私には難しかったのでフルタイムの仕事を辞めたりしましたが、私にとっては大いに意味のある書籍執筆になりました。

その他にも、単著で書きたかった理由とか執筆に関する諸々で感じたこととか語りたいことはたくさんあるので、それはまた別途書きます（多分）。

あと、他の人の本を読むことも好きなので、著者の人となりがありありと感じられるような専門的な技術書がもっと増えるといいなぁと思っています。


### 興味ある人はぜひ買って読んでください！
何はともあれ、せっかく書いたのでぜひ多くの人に読んでもらいたいです。
内容的に誰でも読めるという本ではなく、対象読者層という観点でめちゃくちゃ売れる本ではないと思っていますが、それでもやはり書いたからにはできるだけ売れて欲しいです。
100万冊売れて映画化して欲しいです。

よろしくお願いします！！！！！


### 本書で扱う論文のリスト
本書では、内容に踏み込んで解説する論文と、単にリファレンスとして言及する論文とを区別しています。
本書で内容に踏み込んで解説する論文のリストは以下になります。
私の好みを反映しつつ、生成AIの理解のために重要と思われる論文を取り上げています。

| 論文リスト |
| :--- |
| Attention Is All You Need (2017) [https://arxiv.org/abs/1706.03762v7](https://arxiv.org/abs/1706.03762v7) |
| Contextual correlates of synonymy (1965) [https://dl.acm.org/doi/10.1145/365628.365657](https://dl.acm.org/doi/10.1145/365628.365657) |
| Neural Machine Translation of Rare Words with Subword Units (2015) [https://arxiv.org/abs/1508.07909v5](https://arxiv.org/abs/1508.07909v5) |
| A new algorithm for data compression (1994) [https://dl.acm.org/doi/10.5555/177910.177914](https://dl.acm.org/doi/10.5555/177910.177914) |
| Subword Regularization: Improving Neural Network Translation Models with Multiple Subword Candidates (2018) [https://arxiv.org/abs/1804.10959v1](https://arxiv.org/abs/1804.10959v1) |
| SentencePiece: A simple and language independent subword tokenizer and detokenizer for Neural Text Processing (2018) [https://arxiv.org/abs/1808.06226v1](https://arxiv.org/abs/1808.06226v1) |
| Language models are unsupervised multitask learners (2019) [https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf) |
| Toward a Theory of Tokenization in LLMs (2024) [https://arxiv.org/abs/2404.08335v1](https://arxiv.org/abs/2404.08335v1) |
| Improving language understanding by generative pre-training (2018) [https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf) |
| Language Models are Few-Shot Learners (2020) [https://arxiv.org/abs/2005.14165v4](https://arxiv.org/abs/2005.14165v4) |
| Generating Long Sequences with Sparse Transformers (2019) [https://arxiv.org/abs/1904.10509v1](https://arxiv.org/abs/1904.10509v1) |
| GPT-4 Technical Report (2023) [https://arxiv.org/abs/2303.08774v6](https://arxiv.org/abs/2303.08774v6) |
| A Survey on In-context Learning (2023) [https://arxiv.org/abs/2301.00234v6](https://arxiv.org/abs/2301.00234v6) |
| Why Can GPT Learn In-Context? Language Models Implicitly Perform Gradient Descent as Meta-Optimizers (2022) [https://arxiv.org/abs/2212.10559v3](https://arxiv.org/abs/2212.10559v3) |
| Deep reinforcement learning from human preferences (2017) [https://arxiv.org/abs/1706.03741v4](https://arxiv.org/abs/1706.03741v4) |
| Training language models to follow instructions with human feedback (2022) [https://arxiv.org/abs/2203.02155v1](https://arxiv.org/abs/2203.02155v1) |
| An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale (2020) [https://arxiv.org/abs/2010.11929v2](https://arxiv.org/abs/2010.11929v2) |
| Deep Unsupervised Learning using Nonequilibrium Thermodynamics (2015) [https://arxiv.org/abs/1503.03585v8](https://arxiv.org/abs/1503.03585v8) |
| On the Theory ofStochastic Processes, WithParticular Reference to Applications (1949) [https://digicoll.lib.berkeley.edu/record/112810](https://digicoll.lib.berkeley.edu/record/112810) |
| Denoising Diffusion Probabilistic Models (2020) [https://arxiv.org/abs/2006.11239v2](https://arxiv.org/abs/2006.11239v2) |
| Scalable Diffusion Models with Transformers (2022) [https://arxiv.org/abs/2212.09748v2](https://arxiv.org/abs/2212.09748v2) |
| Learning Transferable Visual Models From Natural Language Supervision (2021) [https://arxiv.org/abs/2103.00020v1](https://arxiv.org/abs/2103.00020v1) |
| Hierarchical Text-Conditional Image Generation with CLIP Latents (2022) [https://arxiv.org/abs/2204.06125v1](https://arxiv.org/abs/2204.06125v1) |
| Imagic: Text-Based Real Image Editing with Diffusion Models (2022) [https://arxiv.org/abs/2210.09276v3](https://arxiv.org/abs/2210.09276v3) |
| Scaling Laws for NeuralLanguage Models (2020) [https://arxiv.org/abs/2001.08361v1](https://arxiv.org/abs/2001.08361v1) |
| Scaling Laws for Autoregressive Generative Modeling (2020) [https://arxiv.org/abs/2010.14701v2](https://arxiv.org/abs/2010.14701v2) |
| DeepSeek-V3 Technical Report (2024) [https://arxiv.org/abs/2412.19437v1](https://arxiv.org/abs/2412.19437v1) |
| Chain-of-Thought Prompting Elicits Reasoning in Large Language Models (2022) [https://arxiv.org/abs/2201.11903v6](https://arxiv.org/abs/2201.11903v6) |
| DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning (2025) [https://arxiv.org/abs/2501.14249v5](https://arxiv.org/abs/2501.14249v5) |
| DeepSeekMath: Pushing the Limits ofMathematicalReasoning in Open Language Models (2024) [https://arxiv.org/abs/2402.03300v3](https://arxiv.org/abs/2402.03300v3) |
| ChatbotArena: An Open Platform for Evaluating LLMs by Human Preference (2024) [https://arxiv.org/abs/2403.04132v1](https://arxiv.org/abs/2403.04132v1) |
| Humanity's Last Exam (2025) [https://arxiv.org/abs/2501.14249v7](https://arxiv.org/abs/2501.14249v7) |
