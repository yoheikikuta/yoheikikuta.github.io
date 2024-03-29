---
title: 令和3年分の確定申告を終えた
description: 令和3年分の確定申告を終えたのでそのふりかえりをしたブログ記事。
pubDate: 2022-02-25
tags: ['雑談']
---


### TL;DR
- 令和3年分の確定申告を終えた
- 仕訳帳を作り始めてから税額が確定してクレジットカードで支払い処理をするまで 6 時間ちょっとだった
- 去年副業とかあまりしてなかったのと特に新しい処理がなかったので過去最短だった
---

偉いので確定申告をした。
特筆すべき点はないのだがメモがてらブログに書いておく。

### 自分の確定申告の流れ
過去に記事 [確定申告の提出書類を作成した](https://yoheikikuta.github.io/blog/2018-02-12-tax_returns/) を書いていて、基本的にはこれを毎年少しずつ育てて（新しいことがあったら情報をアップデートして）いる。

今年の確定申告も例年通り以下の手順で進めた。

- 仕訳帳を作る
- 仕訳帳を基に総勘定元帳を作る
- 株式関連の情報を取得して整理
- e-Tax で確定申告書B、所得税青色申告決算書、医療費向上の明細書、外国税額控除の明細書、を作成
- 内容を確認してクレジットカードで納税

### 昨年から変更が入った分
電子庁保存法 [https://www.nta.go.jp/law/joho-zeikaishaku/sonota/jirei/02.htm](https://www.nta.go.jp/law/joho-zeikaishaku/sonota/jirei/02.htm) というものが2022年1月から施行された。
これは、これまで紙の保管を義務付けられていた国税関係帳簿書類などを電磁的に保存しておけば紙が不要になるもの、と理解している。
まあ正直細かい条件とか読んでないけど、最初に帳簿とかを作るときは全部 Google Sheets で作ってるのでこれで満たされていて欲しい（希望的観測）。

医療費控除のマイナポータル連携で自動的にデータ取得ができるようになった。
これはとりあえず連携してるので試してみたが、ちゃんと全部情報が入ってんのかな？という疑問が湧いた。額を見ると足りない気がする。
どちらにせよ今回は医療費控除が発生するほど医療費使ってないので、連携ができたという以上の深入りはしてない。

あとは e-Tax でスマホからできるよってアピールが強くなってた気がした。
M1 Mac とかで問題なくできるのかなという懸念があったのでうまくいかなかったらスマホで試してみようとも思ったが、問題なくできたので試してない。

そんなもんかな。
昨年は副業をあまりやってないので経費とするものもほとんど発生しないし、作業はサクッと終わった。

### M1 Mac から e-Tax
マイナンバーカードの読み込みがうまくいかないかも、的な警告を目にした気がしたが、結果的に自分は問題なくできた。
ただし Chrome は対応していないので、Safari で処理をした。

- Safari: Version 14.1.2
- IC カードリーダ: NTT ACR39-NTTCom [https://www.ntt.com/business/services/application/authentication/jpki/download6.html](https://www.ntt.com/business/services/application/authentication/jpki/download6.html)
- e-Tax ソフト: 適宜これやれあれやれと指示が出たものに従って特に問題なくできた

### 所管
- トータル 6 時間くらいで終わってよかった（去年は 15 時間くらい掛かってそうだった）
- 外国税額控除のための作業が一番面倒くさい（SBI証券で特定口座（源泉徴収なし）だと年間取引報告書が発行されずに自分で一件一件調べないといけない...過去に問い合わせたときも一覧は作成してないと言われた）
- 色々とめんどくさいところはあるけど、色々調べて自宅で作業して申告と納税をする、という一連の流れが全部自宅で完結できるのは便利だ

### まとめ
令和3年分の確定申告も無事に終えた。偉い。
