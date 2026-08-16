---
title: 書籍「原論文から解き明かす生成AI」発売1周年振り返り
description: 執筆した書籍「原論文から解き明かす生成AI」が発売から1年経ったので振り返りをするというブログ記事。
pubDate: 2026-08-16
tags: ['Machine Learning']
---


### TL;DR
- 書籍「原論文から解き明かす生成AI」発売から 1 年経ったので振り返ってみる
- 内容に関しては狙い通りそれほど陳腐化しておらず、難易度の割には結構売れもしたので成功したと言える結果
- X のポストで 1 年間を振り返ってみたが、こうして眺めてみるとなんやかんや色々あった
---

書籍「原論文から解き明かす生成AI」が発売からほぼ 1 年（発売日は 2025-08-15）が経った。
1 周年記念ということで振り返りのブログを残しておく。

内容について簡単に振り返るととともに、事前に出してもらったご意見に回答をしていくという形にする。
最後に X のポストを引用しつつ様々な出来事を振り返る。


### 内容についての振り返り
すぐに陳腐化する表面的なものではなく長い期間有効である本にしたいと考えていて、今のところそれは達成できているように思う。
この分野は競争が激し過ぎて最先端のトピックはどんどん発展していくので本にするのは適していないが、あまり変わらない土台として学んでおくとよい内容として本書は悪くないのではないだろうか。もっと色々取り上げたい気持ちはあるが。
もちろんまだ 1 年なのでこの先に著しい進化があれば話は変わってくるだろうが、それはそれとして面白いので本書が十分に売れ切ってから進化してほしい（今からそんなに売れないだろという気もするのですぐに進化してもらってもいいのかもしれない）。

明らかに古くなったところもあり、評価のところである。
本書では Chatbot Arena (現在の名称は Arena AI) を取り上げているが、現在ではモデルの性能が上がり過ぎて通常のテキストのやり取りでモデル間の性能を評価するのはかなり難しい。
そのため、新しいモデルが登場して Arena AI の結果を引き合いに出すということは減っていて、具体的で難易度の高いタスクの結果を Artificial Analysis [https://artificialanalysis.ai/](https://artificialanalysis.ai/) から引用することが多い。

もう 1 つ、最も難易度の高いタスクとして Humanity's Last Exam を取り上げている。
本書執筆時点（2025-04-30）における最高性能は OenAI O3 モデルの 20.3% だったが、現在（2025-08-16）における最高性能は Claude Fable 5 (with fallback) の 55.5% である（Artificial Analysis のページから引用）。
驚くべき進化スピードですね。
ただ、こちらに関しては典型的な人間であればほとんど解けない問題ばかりなので、モデルが解けるようになったとしてもこのタスクについて言及すること自体の価値は残り続けるように思う。

その他には、AI エージェントでの利用が普及したが、その観点は本書には含まれていない。
アプリケーション寄りの話なのでそういう文脈での書籍は色々出ているが、ReAct のような論文とかエージェントとして賢く動くための事後学習とかを体系的にガチで解説した書籍が出たら面白そうである。すでに誰か書き始めているかもしれないと思って軽く調べたら、[https://www.oreilly.com/library/view/an-illustrated-guide/9798341662681/](https://www.oreilly.com/library/view/an-illustrated-guide/9798341662681/) とか [https://link.springer.com/book/9789819258291](https://link.springer.com/book/9789819258291) とかを見つけた。

errata を GitHub に公開するというのは気付いたものを追加できるので良かったが、いやあ後から出てくる出てくる。
自分でもチェックしたし AI を使って校正させたりもしたけど、後から出てき過ぎてビビる。
いまの AI であればもっといい感じにチェックしてくれると思うが、このミスの量が人間が書いたという証左になるということですね。

GitHub なら PR で修正案を送れるなと考えて GitHub にしたけど、普通に PR 送るの面倒で送るまでいかない人がほとんどだと思うので、これは全然機能しなかった。
Google Forms とかちょっとしたウェブサイトを作ってすぐ投稿・対応できるようにした方がよかったと思う。
そんな中でも GitHub に直接 PR 送ってくれる方も 1 人だけいて、本当にありがたい限りです。

献本に関しては、自分がもらう時は評価にバイアスが入るという理由で断ってきたが、ダブスタ野郎なので自分が書いた時には多くの方に献本をさせてもらった。
みんな快く引き受けてくれて SNS 上で宣伝をしてくれて本当にありがとうございました。
心を入れ替え、本書を執筆後は献本を受け取ることも少しずつ増やしています。これが社会性です。

内容的には簡単ではないので対象読者はそんなにいないかなと考えていたが、そんな中でも 2 回増刷するくらいには売れたので買ってくれた人ありがとうございます。
自分は結構技術書が好きで、専門性の高い技術書がたくさん世に出るようになってほしいので、そのためにも本書がたくさん売れて同じような企画が通りやすくなってほしい。
それと 100 万冊売れて映画化の夢を諦められないのでよろしくお願いします。


### お便りへの回答
1 周年に先駆けてお便りを募集していたので、その一部を引用してコメントを返します。
ここで取り上げて回答するとよさそうなものを選択的に取り上げているので全部には回答できませんが、ご了承ください。

> LLM の研究を楽しむための基礎を作れたと思っています。楽しい本をありがとうございます。

楽しんでもらえたならよかったです。
土台となる基礎を作るという狙いで書いた本でもあるので、本書の内容を理解していればその後の発展についても追随しやすくなるのではないかと思います。
私自身、本書を執筆する上で勉強して理解を深めたところはその後の発展のキャッチアップに役立っています。

> 大学の研究室（非情報系）の輪読会で使用しています。例題が大変興味深く、いつも学生たちと活発に議論しています。

大学の輪読会で使うというのは本書の読み方として想定していたものの 1 つだったので、実際にそのように使ってくれている方がいてよかったです。

> 当時の研究者がどのようなことを考えていたのかを感じ取れる部分が面白かったです。

> まだ途中ですが、ここまでの所、論文の選択にメッセージ性があって、そこはとてもおもしろく読んでます。ストーリーというか続けて読む事で自分の中でも割と納得感を持って消化していけているし、こんな論文があったのか、という古いが興味深い論文なども知れて、しかも今読むと趣きがあって良い。こういう主張のある本の方が出版される意義を感じます。

> ストーリーがある技術書が好きなので楽しめました。

どういう原論文を取り上げて解説するかは本書の核となるところで、著者の好みとかメッセージが詰め込まれているので、その部分を面白いと思ってくれるなら本望です。
改めて振り返ってみても自分の経験とか好みが大いに反映されていて、他の人ならどの論文を選ぶのかを聞いてみたいですね。

> 練習問題が、解答があって割と簡単でない問題に突っ込んでいるのは良いですね。むしろ本文の解説よりこっちの方が役に立つ事は多い。

演習問題は本書執筆開始時点から入れようと思っていたもので、労力の割には取り組んでもらえることは多くないので書く側にとっては難しさもありますが、役に立つ人がいるということはいい話ですね。
演習問題の設計意図やうまくやれなかったところなどは別途ブログにもしています: [https://yoheikikuta.github.io/blog/2025-09-19-exercise_genai_book/](https://yoheikikuta.github.io/blog/2025-09-19-exercise_genai_book/)

> 本書の解説は良く分からない事も多く結局原典を読む必要がある事が多いけれど、原典を読む時の問題意識を固めるための前準備くらいに活用しています。もっとそう割り切ってしまっても良かったような気も。

狙いとしては、本書だけで原論文の主要なポイントは理解できる、より深掘りしたい場合には原論文や関連論文を読んでもらう（その際に本書で理解した部分が役に立つ）、というものでした。
なので、よく分からない部分が多いというのは著者の力量不足と言えそうです。
重要な論文を取り上げて、その論文を読む際の問題意識や背景知識を解説することで内容を理解できるようにする、という書籍とかも確かに面白そうです。

> ほんの少しだけ工夫すれば、もっと手に取ってもらえると思います。

これはタイトルとかキャッチコピー的な部分に対するコメントで、自分としてはそういう部分にもっと手を入れた方がよかったという気持ちは特にないですが、もっと売れるようにするためにやるべきことあったのではと言われるとおっしゃる通りかなと思います。

> 5.2 拡散モデルが詳細に書かれていてとても良かったです

ここは著者にとって（解析的に色々できて気持ちがいいという意味で）癒しの部分でした。
原論文に沿って解説をしているので、後続研究によって整理された視点を提供できなかった部分は多いですが、そういったものは他の本やレビュー論文などで理解を深めてもらうとよいと思います。

> 経験知が多い（らしい）生成AIのカテゴリをどのように数学的理論付けしていくか、が難しかったです。もちょっと数学勉強します。

> この本のコンセプトが素敵で好きだなと思い、発売直後に買おうと本屋に行ったですが、基礎知識が足りなすぎて立ち読みで挫折してしまったというのが正直なところです。ただその後もう少し基礎を学習してきて、最近向き合えそうになってきた気がするので改めて買います（決意）

本書の対象は学部レベルの機械学習を理解している人なので、理系の学部レベルの数学や機械学習の知識がないと読むのはなかなか難しいかなと思います。
この手のものを独学で学ぶのはかなり大変ですが、最近は AI が賢いので AI と議論しながら自分の理解を深めるという方法が使えるので、独学でも学びやすい時代になったように思います。

> 原典にあたる重要性をあらためて学ぶことができました。こういう書籍が売れる経済社会であって欲しいと思います。

せっかくもっと売れてほしいです！
まだ買ってない人で興味がある方はぜひ！

> 本書ではTransformerやGPT、拡散モデルなど、それぞれの技術が登場した背景から丁寧に説明されていますが、今後の生成AIの発展を理解するうえで、特に優先して継続的に追うべき研究領域や論文があれば、著者の方の考えを伺いたいです。

実に様々な領域が広がっているので、ある程度土台が出来ているならばやはり自分が好きなトピックを追う方がよいと思います。
個人的には reasoning の領域とかモデル評価は面白いなと思いますが、昨今なら AI エージェントとして賢く動くための仕組みや発展などは最も盛り上がっている領域と言えるでしょう。自分の好みにマッチする領域がきっとあるのではないかと思います。

> また、原論文を読む際に、数式を完全に理解してから先へ進むべきなのか、最初は実装や具体例を通して大まかな挙動をつかむべきなのか、理解が難しい論文に取り組む際のおすすめの進め方も知りたいです。

目的次第ですが、実装とか具体例を通じて実際に何かを作って使っていけるようになる方がほとんどの場合で役に立つのではないかと思います。
役に立つ、というのは例えば仕事で活用しやすいとかそういう話を想定しています。
お察し（？）の通り、私は別に役に立つことをそこまで求めていないので、実装は最小限しか取り扱わない本書を執筆しました。

> 加えて、著者の方が最新のLLMを使って、自身の論文理解や学習効率を高めるために実践していることがあれば、ぜひ知りたいです。たとえば、論文を読む際にどのような質問をLLMに投げるのか、数式や実装の理解、関連研究の整理、理解度の確認などに、どのように活用しているのかといった具体的なノウハウにも興味があります。

PDF 丸投げした上で自分が理解できてない観点とか具体例を挙げてもらうなどの使い方をすることが多いです。
論文にはこう書いてるけど自分はこう思うんだけど、とか具体例挙げてもらった上で論文のこの記述とどう対応してるの、とか。
あとシンプルに自分の知識が足りてない領域だとその領域のことを解説してもらうなどもします。
まとめを作ってもらうこともあるんですが、まとめはまとめを作る際に自分で考える過程に一番の学習効果があるので、単純にまとめを作ってもらっても効果をほぼ実感できていないです。色々やりとりをした上で、そのやりとりの部分を中心にまとめてもらうと後から見返す時に有益になりやすいと感じます。

> そのため、次の書籍に収録される前の新しい論文や技術について、書籍よりも短い単位で解説する有料noteやニュースレターのようなコンテンツがあれば、ぜひ購読したいです。本書のように、単なるニュースの紹介ではなく、原論文をもとに背景や技術的な意味まで体系的に解説していただける継続的なコンテンツがあると、とてもありがたいです。

こういうのはやりたい気持ちがありますが、いまの生活状況だとなかなか難しいところです。
子どもたちがもう少し大きくなってきたら、何か自分が継続的に取り組んでいけるコンテンツをやりたいなと思ったりします。

> 退職をして執筆されたとのエピソードも目にし、シンプルにかっこいいなと思いました。

働かなくていい財産があるわけでもなく、家族もいるのに、フルタイムの仕事をしながらだと執筆は無理だからと退職をしているので、あまりかっこよくはないのではないかと思います。そういう状況でも協力をしてくれた妻はかっこいいなと思います。


お便りをくれた方々、ありがとうございました！
ここには書けないようなお便りをくれた方もいて、たいへん興味深かったです。


### X のポストと共に振り返る 1 年間

新着ランキング 1 位になっていたので記念カキコ。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">多くの方が予約や拡散してくれたおかげで、Amazon の本のコンピュータ・IT &gt; コンピュータサイエンス のカテゴリで新着ランキング1位になっていました。<br><br>ありがとうございます！ <a href="https://t.co/kaHT0mQOlx">pic.twitter.com/kaHT0mQOlx</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1950451729616818681?ref_src=twsrc%5Etfw">July 30, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

現物を手に入れた時の様子。テスト販売がこれより早くやっていて著者より先に実物を手に入れる人がいるというのは面白かった。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">ついに著者も「原論文から解き明かす生成AI」を手に入れました。なかなか良い本ですねこれは。<br><br>レビュワーや献本先の方々にも順次届いて読み始めてもらってるので、発売日の 20250818 辺りに感想なども発信してもらえると思います！ <a href="https://t.co/8YBfy9OKVk">pic.twitter.com/8YBfy9OKVk</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1952527978438574535?ref_src=twsrc%5Etfw">August 5, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

書泉ブックタワーで 1 位になっていたので記念カキコ。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">1位すごい🎉 <a href="https://t.co/NOJjqXonhZ">https://t.co/NOJjqXonhZ</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1954773016342409497?ref_src=twsrc%5Etfw">August 11, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

人のアイデアを借りて学生に無料プレゼント企画をした。支援者の方々のおかげもあり最終的に配布可能な人全員（49 人）に配った。
その時の振り返りブログはこちら: [https://yoheikikuta.github.io/blog/2025-09-08-present_genai_book_result/](https://yoheikikuta.github.io/blog/2025-09-08-present_genai_book_result/)
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">書籍「原論文から解き明かす生成AI」を学生にプレゼントします。<br><br>大学院生や意欲のある学部生にも読んでもらいたいですが、金銭的に購入が簡単ではない人もいると思うので、そういう人が対象です。<br><br>詳しくはブログをご覧ください。<br><br>※著者の自腹なので数に限りがあります<a href="https://t.co/Lb6GR6QxvR">https://t.co/Lb6GR6QxvR</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1959067008643088484?ref_src=twsrc%5Etfw">August 23, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

発売日から 3 日で増刷が決まった。買ってくれる人がいるというのはありがたいですね。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">著書「原論文から解き明かす生成AI」ですが、発売日から3日で増刷が決定しました！<br><br>著者としてはそんなにたくさん対象読者がいるのかと新鮮な驚きと若干の戸惑いがありつつも、読んでもらえるのはとても嬉しいです。<br><br>興味があるけどまだ読んでいないという人はぜひどうぞ！ <a href="https://t.co/Wnj4VSkBzD">https://t.co/Wnj4VSkBzD</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1958690869705646297?ref_src=twsrc%5Etfw">August 22, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

Forkwell のオンラインイベントで話した（アーカイブ配信あり）。かなり好き放題話したので面白かった。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">書籍「原論文から解き明かす生成AI」のオンラインイベントを 2025/09/10 12:00~ に開催します。<br><br>Forkwell Library #106 のイベントで、本書の魅力・推しポイントや本書には書かれていない裏話的なエピソードを話す予定です。<br><br>興味がある方はぜひ！<a href="https://t.co/Eiu2lB7Wxz">https://t.co/Eiu2lB7Wxz</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1960134748644552824?ref_src=twsrc%5Etfw">August 26, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

発売後 1 ヶ月で本屋に実物を見に行った。色々あって遅くなってしまった。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">発売後1ヶ月経って、ようやく自分の足で書店に並んでるのを拝んできた。<br><br>宣伝のために、立ち読みしながら「うわあ、なんてクールな本なんだろう！！！」って独り言を言ってきました。 <a href="https://t.co/JoGr2quvWC">pic.twitter.com/JoGr2quvWC</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1967852599459319974?ref_src=twsrc%5Etfw">September 16, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

大学生協でも月間売り上げ 1 位になった。学生がじっくり読むのに良い本になるというのは一つの目標だったので売れてくれてよかった。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">大学生協でも「原論文から解き明かす生成AI」を取り扱ってくれていてありがたい🙏<br><br>学部生だと読むのは少し難しいかもしれませんが、良い経験になると思うのでぜひチャレンジしてみて欲しいです。 <a href="https://t.co/DcbuZkScGB">https://t.co/DcbuZkScGB</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1968643081755836908?ref_src=twsrc%5Etfw">September 18, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

演習問題の設計思想についてブログに書いた。演習問題までやる人はほとんどいないとは思っていたが、解答を全部準備することも含めて頑張ったところなのでそのアピール。たまに演習問題に言及してくれる人がいて、そういう人には好評なのでよかった。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">書籍「原論文から解き明かす生成AI」の演習問題の設計の話を書きました。<br>頑張って演習問題とそのすべての解答を準備したので、興味ある人は解いてみてねという宣伝です。<a href="https://t.co/IGHboidbe9">https://t.co/IGHboidbe9</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1969199424686490008?ref_src=twsrc%5Etfw">September 20, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

第 3 刷の増刷が決まった時のポスト。ちなみに本を買ったと言ってくれる人は結構いますが、本を読んだと言ってくれる人はそんなにいません（読むの大変ですよね分かります）。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">著書「原論文から解き明かす生成AI」ですが、第3刷の増刷が決まりました！<br><br>読むのが簡単な本ではないですが、多くの方に買っていただいているようで嬉しい限りです。<br><br>書籍に関する忌憚のない意見も大歓迎ですので、SNS やブログや Amazon レビューなどもお待ちしております。 <a href="https://t.co/RhHVogtc0R">https://t.co/RhHVogtc0R</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1970786741205532854?ref_src=twsrc%5Etfw">September 24, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>


書泉ブックタワーで選書フェアをやってコメントなどを書きに行った。動画撮影してる時に見てる人がいて、終わったら話しかけられた本を買うのでサインしてくれと言われてサインした。なんかすごい人と勘違いさせてしまったかもしれない。他にもジュンク堂（池袋本店や大阪本店）でも選書フェアをやった。
<div align="center">
<blockquote class="twitter-tweet" data-media-max-width="560"><p lang="ja" dir="ltr">書泉ブックタワーで開催中の選書フェアを紹介している貴重映像です。<br>菊田遥平先生（実態はただのほぼ無職）の選書フェアが気になる方はぜひお立ち寄りください。 <a href="https://t.co/YbqBTf2dcS">https://t.co/YbqBTf2dcS</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1972616348112208213?ref_src=twsrc%5Etfw">September 29, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

kindle 版が 50% ポイント還元になった時のポスト。ポイント還元については著者には何の情報も知らされない（全部知らせるというのは非現実的だが）ので人のポストで知った。その後 67% ポイント還元も発生した。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">著者もこちらの post で知りましたが、「原論文から解き明かす生成AI」の kindle 版が 50% 還元ポイントキャンペーン中です！<br><br>¥3,234 で 1,617pt 得られるので、まだ購入してなくて興味がある方はこの機会に是非どうぞ！！！<a href="https://t.co/Qozy7ZoNdL">https://t.co/Qozy7ZoNdL</a> <a href="https://t.co/vEFZ3fpRFm">https://t.co/vEFZ3fpRFm</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1995663125295907226?ref_src=twsrc%5Etfw">December 2, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

Lancers のオンラインイベントで話した。こういうイベントをキャッチして聴きにきてくれる人がいるというのはありがいことです。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">明日のお昼にこのイベントで話します。<br>興味ある方はご飯食べながらどうぞ。<a href="https://t.co/PMhPcaL73K">https://t.co/PMhPcaL73K</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/1998376069091778782?ref_src=twsrc%5Etfw">December 9, 2025</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

kindle の機能で他の人がどこに多くハイライトしているのかを知れる機能を知った時のポスト。微分操作ができないのは恐ろしいですよね。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">「原論文から解き明かす生成AI」のKindle版の67%ポイント還元はまだやっているようです。<br>いつまで続くのか分かってないですが、まだ購入してない方はぜひ！<br><br>KindleにはPopular Hilightsの機能があって他の人がハイライトした部分が見れますが、私が見たところこれが一番ハイライトされてました。 <a href="https://t.co/QcqrCOx1YQ">pic.twitter.com/QcqrCOx1YQ</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/2009981654803403248?ref_src=twsrc%5Etfw">January 10, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

早川書房 x 技術評論者の共同フェアに取り上げられた時のポスト。SF の本とセットで技術書を紹介するという企画で、自分の本はテッド・チャン「息吹」とのセットだったのでコメントを書くために読んでみた。小説を久しぶりに読んで面白かった。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">早川書房 × 技術評論社の共同フェア「AI誕生70周年 AIはどんな夢をみてきたか」で私の著書『原論文から解き明かす生成AI』も取り上げられています。<a href="https://t.co/TRgcGIeEAD">https://t.co/TRgcGIeEAD</a><br><br>著書コメントを書くためにテッド・チャン『息吹』を読みましたが、面白かったです。 <a href="https://t.co/zqvKtmd6UP">https://t.co/zqvKtmd6UP</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/2072610214545957088?ref_src=twsrc%5Etfw">July 2, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>

1 周年振り返りブログを書こうと思い、お便り募集をした。1 年前の本にコメントを寄せていただいた方、ありがとうございました。
<div align="center">
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">【拡散希望】<br>著書『原論文から解き明かす生成AI』ですが、もうすぐ発売から一年経ちます。振り返りをしようかなと考え、その際に色々な人からの感想などがあると嬉しいなと思い、匿名アンケートを作成しました。<br>二問だけのアンケートなので、答えてもらえると嬉しいです！<a href="https://t.co/T0Hj5gxwK9">https://t.co/T0Hj5gxwK9</a></p>&mdash; Yohei KIKUTA / 原論文から解き明かす生成AI 8月18日発売 (@yohei_kikuta) <a href="https://x.com/yohei_kikuta/status/2081353051462672483?ref_src=twsrc%5Etfw">July 26, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
</div>
