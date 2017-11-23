---
title: 解答例_課題PH1
date: 2017-11-23 21:34:57
tags: [N, Education, mOeKa]
---
```
Provided By mOeKa
```

# 課題1

## VirtualBox5.2をインストール

ググって普通にインストール


## CentOS6.9をインストール

[CentOS6.9 x86-64 ミラーサイト](http://ftp.yz.yamagata-u.ac.jp/pub/linux/centos/6.9/isos/x86_64/)
より
`CentOS-6.9-x84_64-bin-DVD1.iso`をダウンロード

参考：
[ContOS6.9をVirtualBoxにインストールしてlempサーバーを構築する](https://www.hbirds.net/linux/centos6-9%E3%82%92virtualbox%E3%81%AB%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%81%A6lemp%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E3%82%92%E6%A7%8B%E7%AF%89%E3%81%99%E3%82%8B/25434v)  
参考：
[【超初心者Linux】第1夜：MacにVirtualBoxでCentOSをインストールする
](http://dogandrun.hatenablog.jp/entry/2013/10/16/104825)

### VirtualBoxで設定
<details>
<summary>OSの設定内容</summary>
- 名前：CentOS6.9  
- タイプ：Linux   
- バージョン：Red Hat(64bit)  
- メモリ：1024MB  
- 仮想ハードディスクサイズ：20GB
</details>

<details>
<summary>~~ネットワークの設定~~</summary>
<s>
[設定]>[ネットワーク]より割り当てをブリッジアダプターに変更。  
これによりMac（ホストOS）とCentOS（ゲストOS）を、それぞれ同じネットワーク内で、異なるIPを持つ独立したコンピュータとして動かせるようになる。らしい。
</s>
</details>

<font color="MediumVioletRed">
！注意！  
ネットワークの設定は上の設定だと、
後のHostOSとの通信でうまくいかない。  
[ここ](#networkconf)を参照して設定すること。
</font>



### CentOSのインストール
NICの設定で、IPv4の割り当てを手動にし、ホストOSのIPアドレスの第四ブロックを変えたIPアドレスに設定


## CentOSにApache2.4をインストール

<details>
<summary>yum(Yellowdog Updater Modified)とは</summary>  
役割としてはRPMパッケージを統合管理するというものだ。  
RPM単体ではパッケージ情報、依存関係などの情報を持ち合わせているものの、それを統合的に管理運用するシステムがない。
ユーザの手間を減らすためにできたのがYUMだ。  
YUMはRPMの情報を管理し統合、依存関係を自動的に解決してくれる。
DebianでいうところのAPTと同じ立ち位置になる。  
**YUMを使用することでディストリビューションのパッケージアップデートやパッケージの検索、パッケージ削除、パッケージの情報表示などができるようになる。**
</details>
[【初心者でもわかる】yumコマンドの使い方とリポジトリの追加方法](https://eng-entrance.com/linux-package-yum)

<details>
<summary>RPM（Redhat Package Manager）パッケージとは</summary>  
Red Hat系のLinuxやTurbolinuxでは、**プログラムの配布形式** としてRPMを採用している。
これにより、ソフトウェアのインストールやアップデート、アンインストールが非常に簡単に行える。
RPMパッケージには、プログラムなどのバイナリファイルや設定ファイル、ドキュメントなどがまとめられており、rpmというコマンドでインストールや削除などの操作ができる。
</details>


### インストール方法
参考：[[Apache2.4] yum経由でApache2.4 をインストールしてPHP5.6を動かすまで](https://qiita.com/pb_tmz08/items/edd737affa0e2671d422)  
参考：[CentOS 6.x に、Apache2.4とPHP 5.6をインストールする](https://ex1.m-yabe.com/archives/2962)

<font color="MediumVioletRed">
！注意！
CentOSにはデフォルトでApache2.2系が入っている。Apache2.4系を入れても、気がついたら2.2を設定、起動していたという事態が発生する。上のリンク先の指示にきちんと従うと未然に防ぐことができるので、ちゃんと2.2系を削除したり2.4系にシンボリックリンクを貼り直したりすること。  
</font>

<font color="RosyBrown">
Userをrootではなくmoekaでやっていたので、上記サイトのコマンドそのままではできなかった。  
wgetやyumコマンドの前にsudoをつけて管理者で実行すればよかったが、moekaにsudo権限がなかったので、
[CentOSでuserをsudo可能にする](https://qiita.com/Esfahan/items/a159753d156d23baf180)で権限をつけた。
</font>


### 起動方法

```sh
# Apache2.4を起動
service httpd24-httpd start
```


## MacからゲストOSにHTTPで接続できるようにする

### ファイアウォールを無効化
参考：
[ファイアウォールiptablesを簡単解説～初心者でもよくわかる！VPSによるWebサーバー運用講座(4)](https://knowledge.sakura.ad.jp/4048/)  
参考：
[CentOS6:ファイアウォール](https://www.server-world.info/query?os=CentOS_6&p=initial_conf&f=2)

```sh
# ファイアウォール無効化
/etc/rc.d/init.d/iptables stop

# 自動起動設定をオフに
chkconfig iptables off
```

<a id="networkconf"></a>
### ネットワーク設定
参照：
[VirtualBox CentOS6.7 64bitでNAT、ホストオンリーアダプターを使用](http://www.kakiro-web.com/memo/virtualbox-create-virtual-machine-centos6-2.html)  
参照：
[今さらながらVirtualBoxネットワーク設定のベストプラクティスと解説](https://qiita.com/mokrai/items/ea35094c5dc4699d2a6b)


- VirtualBoxのGrobal toolsからホストオンリーネットワークをホストOSに作る
	- アダプター
>IPv4 : 192.168.56.1  
>ネットマスク : 225.225.225.0  

  - DHCP
>サーバアドレス : 192.168.56.100  
>サーバマスク : 225.225.225.0  
>アドレス下限 : 192.168.56.101
>アドレス上限 : 192.168.56.254

	こっちの設定は、ゲストOSの方に割り振られるアドレス。
	**固定の方が使い勝手がいいという話もあるので、後で固定にしたい。**

- ゲストOSの[設定]>[ネットワーク]>[アダプター2]を有効化、割り当てをNATに  
- ゲストOSの[設定]>[ネットワーク]>[アダプター3]を有効化、割り当てをホストオンリーネットワークに  
<font color="RosyBrown">※OSインストール時にブリッジアダプターをeth0にしてしまっていたので、アダプター1は無効化して放置</font>

- 下記のファイルを配置

	```php:etc/sysconfig/network-scripts/ifcfg-eth1
	DEVICE=eth1
	TYPE=Ethernet
	ONBOOT=yes
	BOOTPROTO=dhcp
	NAME="System eth1"
	```
	```php:etc/sysconfig/network-scripts/ifcfg-eth2
	DEVICE=eth2
	TYPE=Ethernet
	ONBOOT=yes
	BOOTPROTO=dhcp
	NAME="System eth2"
	# NetworkManagerを無効化
	NM_CONTROLLED=no
	```
	NetworkManagerを無効化しているのは下記と同じ状況になったため。  
	[Error: Connection activation failed: The connection is not for this device.](http://mylinuxnotes.com/tips-and-tricks/error-connection-activation-failed-the-connection-is-not-for-this-device/)

- ネットワークサービスを起動  

	```sh
	 service network start
	```



##  MacからゲストOSに立てたサーバのWebサイトを見る

### DocumentRootにページを配置
以下にテストページを配置

```html:/var/www/html24/test/index.html
<html>
<header>
<title>test page</title>
</header>

<body>
Hello world!
</body>
</html>
```
/var/www/html24/ -> /opt/rh/httpd24/root/var/www/html


### Macから名前解決
macのターミナルを起動し、以下のファイルを編集

```php:etc/hosts
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1	localhost
255.255.255.255	broadcasthost

# この行を追加！！
192.168.56.101 nxxxl-test.com

::1             localhost

```
`192.168.56.101`は、CentOSで

```sh
ifconfig
```
ででてきた中の、
eth2(ホストオンリーネットワーク)の`inet addr`に書かれているアドレスと合わせる。

### Macで表示
Mac内のブラウザで  
`http://nxxxl-test.com/test/`  
でアクセスして、「Hello world!」と表示されたら成功！
