---
title: jekyllで作成したページをローカルでプレビューする
description: jekyll でブログを書いているが、local 環境で serve して確認する時の環境構築過程を記録したブログ記事。
pubDate: 2017-01-17
tags: ['env development']
---

### TL;DR
- Ubuntu Desktop 環境で jekyll serve を使えるようにした
<br>

UbuntuでGithub Pagesに公開するjekyllで作成したサイトをローカルで確認できるようになることが目標。
ちなみにUbuntu 16.04 LTS。

### rbenvを用いたRuby環境の構築
version management toolであるrbenvを用いてRuby環境を構築する。  
まずは必要な依存関係のあるパッケージをインストール。

```bash
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev nodejs
```

必要なrepositoryをcloneしてpathを通す。

```bash
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
```

Rubyをインストールする。とりあえずglobalの環境も2.4.0にしておくが、この辺は好みで。

```bash
rbenv install 2.4.0
rbenv global 2.4.0
ruby -v
# ruby 2.4.0p0 (2016-12-24 revision 57164) [x86_64-linux]
```

最後に3rd party製のlibraryを管理するためのgemを扱うのに有用なbundlerを入れておく。

```bash
gem install bundler
```

### Railsをインストール
Railsでアプリケーションを動かすために必要になるNode.jsもインストールする。

```bash
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
gem install rails -v 5.0.1
rbenv rehash
rails -v
# Rails 5.0.1
```

### jekyllとgithub-pagesのインストール
これも素直に入れるだけ。

```bash
gem install jekyll
gem install github-pages
```

### repositoryをcloneしてきてローカルで確認
自分の場合はこんな感じ。

```bash
git clone https://github.com/yoheikikuta/yoheikikuta.github.io.git
cd yoheikikuta.github.io/
jekyll serve
#Configuration file: /home/yohei/git/yoheikikuta.github.io/_config.yml
# ...
#    Server address: http://127.0.0.1:4000/
#...
```

これでブラウザで [http://127.0.0.1:4000/](http://127.0.0.1:4000/) にアクセスすれば確認できる。  
止める場合は ```Ctrl+c``` で止める。ちなみに起動中にファイルを変更して保存すると自動的にウェブページの再生成が走るので、ブラウザをリロードすれば変更を確認できる。

最も基本的な使い方はこんなもんでしょうか。

---
20180728 追記  
結局ローカルで環境構築をするのが大変なので、docker を使うことにした。
自分で色々いじってたがなんか gem でうまくいかなかったりしていたところ、[https://github.com/envygeeks/jekyll-docker](https://github.com/envygeeks/jekyll-docker) を見つけた。  
`xxx.github.io` の top directory で以下を実行すればよい。

```bash
docker run -it --rm -p 4000:4000 -v $(pwd):/srv/jekyll jekyll/jekyll jekyll serve
```

ありがとうございます。
