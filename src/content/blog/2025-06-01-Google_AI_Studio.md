---
title: Google AI Studio が提供する機能
description: Google AI Studio とはどういう立ち位置でどんなサービスを提供しているのかをまとめるブログ記事。
pubDate: 2025-06-01
tags: ['Machine Learning']
---

### TL;DR
- Google AI Studio [https://aistudio.google.com/](https://aistudio.google.com/) は開発者や AI 実験者向けのプラットフォーム
- 生成 AI に関する新しい技術をほとんど無料で使うことができる（API 利用は有料）
- 2025年1月に AI Studio チームが Google DeepMind に移ることになったので、より一層サービス提供が加速されていきそう
---

Google AI Studio [https://aistudio.google.com/](https://aistudio.google.com/) は様々な機能を提供していて把握しきれてないので、備忘のために2025年6月1日時点の情報をまとめておく。

Google AI Studio は開発者や実務者向けのプラットフォームで、Google が開発する AI 機能をほとんど無料で使うことができる。
OpenAI Platform Playground [https://platform.openai.com/playground](https://platform.openai.com/playground) を知っていれば、Google AI Studio は大体これと同じような役割だと思っておけばいいだろう。


### Google AI Studio の機能
2025年6月1日時点で提供されている機能をまとめておく。
全て無料で使えるが、これらの機能とは別に API Key の作成が可能になっており、これを介して Gemini API が利用可能である。
Gemini API に関しては [https://ai.google.dev/gemini-api/docs](https://ai.google.dev/gemini-api/docs) に書かれている。

#### Chat
典型的な LLM 利用のためのツールだが、やれることは多い。
各種モデルの選択・System Instruction の設定・2つのモデルで出力を比較・softmax における temperature や核サンプリングにおける Top Pなどのパラメータ設定、などなどができる。
また、Tools として Structured Output を指定したり、URL context でウェブ検索をしたりもできるので、LLM の振る舞いを変えながら色々試せるのは面白い。

<center>
<a href="https://imgur.com/p9qkns5"><img src="https://imgur.com/p9qkns5.png" title="source: imgur.com" width="800" /></a>
</center>

このような機能は OpenAI Platform Playground とほとんど同じであるので特に目新しいものはないが、使える機能は微妙に違っていたりする。
例えば、OpenAI Platform Playground では MCP Server が使えて、Google AI Studio では Grounding with Google Search というモデルの出力を情報源と紐付ける機能が使えたりする。

#### Stream
音声での対話ができ、こちらも例えばコンテキストサイズを変更するなどのオプションを操作しながら使うことができる。
マルチモーダルなモデルになっているので、Webcam や Share Screen で視覚情報を与えてそれに基づいて音声でやりとりすることができる。

#### Generate Media
テキストや画像や音声の生成ができる。

- Gemini Image Generation
  - これは通常のマルチモーダル LLM で画像生成もできることを述べていて、Chat に遷移する。
- Gemini Speech Generation
  - テキストを入力としてそのテキストの音声を生成する Text to Speech で、single/multi speaker に対応している。
- Imagen
  - テキストを入力として画像を生成する Text to Image で、モデルは Imagen 3 を使える（Chatbot Arena でランキングトップのモデル）。
- Veo
  - テキストを入力として動画を生成する Text to Video で、モデルは Veo 2 を使える（より新しいモデルである Veo 3 は後述のように Google Labs の方だと使えたりするが、Google AI Studio だとまだ使えない）。
- Lyria RealTime
  - 音楽のリアルタイム生成で、Bossa Nova とか音楽の要素を追加すると音楽が自動で生成されるものになっている。

最後の音楽のリアルタイム音楽生成はやや毛色が異なるのでイメージがしづらいが、以下のようにつまみをインタラクティブに操作して音楽が生成されるものになっている（自分はちょっと触って試してみた程度なので、何がどこまでできるかとかは詳しくは知らない）。
ちなみにこのアプリケーションは後述の Build 機能で作ったもの（コードも読める）で、Lyria Realtime のモデルを使っているものである。
Google DeepMind による情報は [https://deepmind.google/models/lyria/realtime/](https://deepmind.google/models/lyria/realtime/) で、上記の生成モデルの並びに入るくらいなので結構力を入れているように感じる。

<center>
<a href="https://imgur.com/X60kdk6"><img src="https://imgur.com/X60kdk6.png" title="source: imgur.com" width="800" /></a>
</center>


#### Build
自然言語によってアプリケーションを作成することができる。
それ自体は色々なサービスで実現されているので特筆すべきものでもないが、AI Studio ではボタンひとつで Cloud Run にアプリケーションをデプロイできるというのを売りにしている。

自分でも試してみたが、確かに一発で Cloud Run にデプロイまでできるのはちょっとしたアプリケーションを作って公開するのには便利である。
ちなみに Google AI Studio でデプロイしたものは以下のように `Deployed from AI Studio` とつくようだ。

<center>
<a href="https://imgur.com/WJ2vPkd"><img src="https://imgur.com/WJ2vPkd.png" title="source: imgur.com" width="800" /></a>
</center>


### Gemini app との違い
Gemini app [https://gemini.google.com/app](https://gemini.google.com/app) との違いは少し分かりづらい。
Gemini app は AI アシスタントサービスで、チャットや動画生成や Deep Research などの機能を提供している。
Gemini は生成 AI モデルのモデル名でもあったり、Google AI Studio でもここで挙げたのと同様の機能（Deep Researchは使えないが）が使えるのは少し混乱しやすいポイントである。

Gemini はかなり絞られたサービスだけが利用可能だが、Google AI Studio はより広く AI に関する様々な機能を提供している。


### Google Labs との違い
Google くらい大きな会社だと様々な取り組みをしていて、AI に限らず開発中の新機能やサービスを試せる Google Labs [https://labs.google/](https://labs.google/) というものもある。

AI に限らずと言っても AI に関するものが多く、2025年6月1日時点では例えば以下のようなサービスが試せる。

- 動画生成 Flow [https://labs.google/flow/about](https://labs.google/flow/about)
- コーディングエージェント Jules [https://jules.google/](https://jules.google/)
- 自然言語で UI デザインとフロントエンドコードを作成する Stitch [https://stitch.withgoogle.com/](https://stitch.withgoogle.com/)

Google AI Studio では使えない機能（例えば Jules）や Google AI Studio よりも先んじて最新モデルが使える場合（例えば動画生成で Veo 3）もあるので、新しい機能を使ってみたい人はこのページの存在を知っておくと楽しめる。
いまや独立したサービスとして有名になっている NotebookLM も元々は Google Labs で提供されたもの [https://blog.google/technology/ai/notebooklm-google-ai/](https://blog.google/technology/ai/notebooklm-google-ai/) だった。

遊び心があるサービスもあるが、個人的に結構好きなのは、Say What You See [https://artsandculture.google.com/experiment/say-what-you-see/jwG3m7wQShZngw](https://artsandculture.google.com/experiment/say-what-you-see/jwG3m7wQShZngw) という、お題の画像を生成するようなプロンプトを考えるゲームである。
プロンプトを書くとそのプロンプトに応じて画像を生成し、生成された画像がお題の画像と指定された類似度よりも高ければクリアというもの。
モデルの気持ちになってプロンプトを考えることができるので面白い（レベルが上がると類似度判定をクリアするのがかなり難しい）。

<center>
<a href="https://imgur.com/rcrx31P"><img src="https://imgur.com/rcrx31P.png" title="source: imgur.com" width="800" /></a>
</center>

一方で、Google Labs で提供されているサービスの利用には Google AI Ultra などの有料プランや waitlist に登録が必要なもの（個人的な体験として waitlist 登録しても全然使えるようにならないので辛い）があったりするので、使いたいと思っても状況によっては使えないものもある。


### Google AI Studio の今後
SNS などで話題になっていたが、2025年1月に Google AI Studio（と Gemini Developer API）チームが Google DeepMind に移った。

<center>
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Today I am happy to share that Google AI Studio and the Gemini Developer API (along with our teams) are moving over to <a href="https://twitter.com/GoogleDeepMind?ref_src=twsrc%5Etfw">@GoogleDeepMind</a>! <br><br>This move will allow us to double down on our already deep collaboration and accelerate the research to developer pipeline. Time to build!</p>&mdash; Logan Kilpatrick (@OfficialLoganK) <a href="https://twitter.com/OfficialLoganK/status/1877389403393290672?ref_src=twsrc%5Etfw">January 9, 2025</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</center>

これにより、Google DeepMind の研究成果がより積極的に Google AI Studio などで利用可能になるものと期待されている。
Google DeepMind はこれまでも多くの素晴らしい研究をしてきており、そのうちのいくつかはサービスとして提供されているが、それが加速されるとなると今後が楽しみである。
