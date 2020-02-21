# bsdinstall

FreeBSD で installerconfig を使ってインストールする人のためのパッチです。現
時点では bsdinstall に以下の不具合があるので、ZFS で bootpool と zroot を分
けてインストールするとうまくインストールされませんので、このパッチを当ててく
ださい。なお、これは既に [Bug 229628](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=229628#attach_194980)
に報告済みです。

## バグの内容

#### 1. /boot -> /bootpool にシンボリックリンクが張られた状態で

	# tar - xf distrubution_tarball - C chroot_directory

で展開されるので、/bootpool 内に入らない。これを回避するには tar に -P オプ
ションを追加する必要がある。

#### 2. デフォルトでは bootpool の zpool.cache 情報が含まれませんので、起動
時に bootpool がインポートされません。これを回避するには zpool.cache に
zroot および bootpool を zpool.cache に書き込む必要があります。
