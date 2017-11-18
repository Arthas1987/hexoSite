---
title: 解答例_課題PH2
date: 2017-11-18 22:47:57
tags: N-Education, Moe
---
```
Provided By mOeKa
```

# 課題2
## ユーザの作成
[Linuxグループの設定方法まとめ](https://eng-entrance.com/linux-group)

```bash
## グループを作成
groupadd GrpA
groupadd GrpB
groupadd Manager

## ユーザを作成
# -g -> プライマリグループを指定（デフォルトだとユーザ名のグループになる）
useradd -g GrpA A-taro
passwd A-taro
# passwd is 'taro'
useradd -g GrpA A-jiro
passwd A-jiro
# passwd is 'jiro'
useradd -g GrpB B-sasuke
passwd B-sasuke
# passwd is 'sasuke'

## B-sasuke を Manager グループに追加
# usermod -> userを修正する
# -G -> セカンダリグループのリストを変更する
# -aG -> セカンダリグループのリストに追加する
usermod -aG Manager B-sasuke

## B-sasuke に sudo権限をつける
usermod -aG wheel B-sasuke
```

### sudo権限
sudo権限設定は、`/etc/sudoers`に記載されている。  
CentOSでは、wheelグループに所属しているユーザがsudo権限を使えるようになっているが、それは`/etc/sudoers`に以下のような記載があるからだ。  

[visudoでsudo権限の設定をする際のメモ](https://qiita.com/kmikmy/items/6a6a086f6415d9b55b96)

```bash
## Allows people in group wheel to run all commands
%wheel ALL = (ALL)		ALL

## Same thing without password
%wheel ALL = (ALL)		NOPASSWORD:ALL
```



## パーミッション設定
[ファイルのパーミッション設定、ディレクトリは要注意](http://wordpress.honobono-life.info/lin-base/%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E3%83%91%E3%83%BC%E3%83%9F%E3%83%83%E3%82%B7%E3%83%A7%E3%83%B3%E8%A8%AD%E5%AE%9A%E3%80%81%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E3%81%AF/)  
[Linux：chownでファイルやディレクトリの所有者を変更する](http://raining.bear-life.com/linux/chown%E3%81%A7%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%84%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E3%81%AE%E6%89%80%E6%9C%89%E8%80%85%E3%82%92%E5%A4%89%E6%9B%B4%E3%81%99%E3%82%8B)  

```bash
## /tmp/taroDir
# 作成
cd /tmp
mkdir taroDir
# 所有者、所有グループを変更
# -R -> ディレクトリ以下のファイルなども全て設定
chown -R A-taro:GrpA taroDir
# 権限設定。所有者、所有グループは書き込み可能。それ以外はアクセス不可
chmod 770 taroDir

# 確認
ls -al | grep taroDir
# drwxrwx---  2 A-taro GrpA  4096 11月 12 09:46 2017 taroDir
```
```bash
## /tmp/taroDir/secret
cd taroDir
mkdir secret
chown -R A-taro:GrpA secret
# A-taro以外はアクセス不可
chmod 700 secret

# 確認
ls -al
# drwx------  2 A-taro GrpA  4096 11月 12 10:08 2017 secret
```
```bash
## /tmp/jiroDir
cd /tmp
mkdir jiroDir
# 誰でもアクセス・書き込み可能
chmod 777 jiroDir

# 確認
ls -al | grep jiroDir
# drwxrwxrwx  2 root root  4096 11月 12 10:10 2017 jiroDir
```
```bash
## /tmp/sasukeDir -> /tmp/taroDir (シンボリックリンク)作成
ln -s /tmp/taroDir /tmp/sasukeDir

# 確認
ll /tmp | grep sasukeDir
# lrwxrwxrwx 1 root root	12 11月 12 10:34 2017 sasukeDir -> /tmp/taroDir

```
