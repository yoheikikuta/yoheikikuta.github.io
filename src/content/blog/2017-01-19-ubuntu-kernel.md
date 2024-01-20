---
title: ubuntuでlinux kernelのversionを固定する
description: ubuntu で nvidi-docker を使うときに不整合が起きてしまったのでそれを回避するために linux kernel version を固体するようにしたというブログ記事。。
pubDate: 2017-01-19
tags: ['env development']
---

### TL;DR
- nvidia-docker と不整合を起こさないように linux kernel version を固定するようにした
---

Ubuntu 16.04 LTSでlinux kernelのversionを固定する。
apt-get upgradeとかでkernelがversion upしてNVIDIAのdriverのversionと不整合を起こして入れ直し、が面倒だというのが主な理由。
こんなもん調べればいくらでも記事が出てくるだろうが、自分用に記録しておく。

### 現在使っているkernel versionを調べる
これは `aptitude` を使うのが楽。なければおもむろに `sudo apt-get install aptitude` で入れておく。

```
$ aptitude show linux-generic
Package: linux-generic
State: installed
Automatically installed: no
Version: 4.4.0.59.62
Priority: optional
Section: kernel
Maintainer: Ubuntu Kernel Team <kernel-team@lists.ubuntu.com>
Architecture: amd64
Uncompressed Size: 12.3 k
Depends: linux-image-generic (= 4.4.0.59.62), linux-headers-generic (= 4.4.0.59.62)
Conflicts: linux-generic:i386
Description: Complete Generic Linux kernel and headers
 This package will always depend on the latest complete generic Linux kernel and headers.
```


### versionを固定する設定ファイルを記載する
versionは上記コマンドで調べたものとする。
書き込むにはroot権限が必要なので `sudo vim /etc/cat/preferences.d/linux-kernel.pref` とかで編集。


```
Package: linux-generic
Pin: version 4.4.0.59.62
Pin-Priority: 1001

Package: linux-headers-generic
Pin: version 4.4.0.59.62
Pin-Priority: 1001

Package: linux-image-generic
Pin: version 4.4.0.59.62
Pin-Priority: 1001
```

だん。これで安心。
