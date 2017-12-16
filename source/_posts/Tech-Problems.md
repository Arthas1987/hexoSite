---
title: 【WIP】技術勉強向けの課題
date: 2017-11-11 17:50:55
tags: [Education, N]
---
# 初めに
## Work In Progress!
このページはWIPである。 作成済の項目は、【WIP】マークを取る。

## 想定作業環境
* CentOS 6 又は 7
> ローカル仮想マシンでもOK  
* Apache 2.4
* Tomcat 8

## 習得してもらいたい知識

### Linux
* 基本コマンド
* パーミッション制御
* ユーザー管理
* 正規表現
* シェル
* スケジューリングタスク作成

### Apache
* 基本設定ファイルの記述方法
* Virtual Host
* アクセス制御

### HTML
* JSの書き方
* CSSの書き方

### その他
* HTTP、HTTPSの通信仕組み
* リモートAPIのコール

# 技術課題
## 技術課題PH1
すでに解決済の為、実施したことのみ記述
### ~~仮想マシン立ち上げ~~
### ~~Apache 2.4環境構築~~
### ~~ホストマシンとの疎通確認~~

## 技術課題PH2
### PH2習得目標
* Linux環境にてユーザーグループの管理
* Linux環境でのパーミッション制御
* 管理者権限コントロールの考え方

### PH2-1 下記の３つユーザーを作成してください
|No|ユーザー名|ユーザーグループ|
|:-----|:--------|:-----------|
|1 | A-taro  | GrpA  |
|2   |A-jiro   | GrpA  |
|3   |B-sasuke   |GrpBとManager  |

### PH2-2　下記のユーザーは、sudoコマンドを実行できるように設定してください
* B-sasuke

### PH2-3 下記の*フォルダ*を作成してください
備考：アクセスは `cd` や `ls` を実行できる意味である。


|No|パス|要件|
|:-----|:--------|:-----------|
| 1  | /tmp/taroDir  | 1.同じグループの人に書き込む権限が必要 <br> 2.グループ以外の人に、アクセス禁止  |
| 2  | /tmp/taroDir/secret  | 1. `A-taro` 以外はアクセス禁止 |
| 3   | /tmp/jiroDir  | 1. 誰でもアクセス、書き込み可能  |
| 4   | /tmp/sasukeDir  | 1. taroDirのシンボリックリンク(`ハードリンク`ではない)  |

## 技術課題PH3
### PH3習得目標
* Apache基本設定ファイルの記述方法
* ApacheのVirtual Host仕組み
* Apacheのアクセス制御
* 備考：なるべく`.htaccess`を利用しないように解答してみてください

### PH3-1 ベーシック制御
下記のリンクへアクセスする際に、パスワード制御をかけてください：  
[/test/](http://nxxxl-test.com/test/)


### PH3-2 リダイレクト
下記の要件で、ページを作成し直してください  
* `/test1/index.html`を作成してください
* `/test2/index.html`を作成してください
* `/test/` へアクセスする際に、ブラウザにて表示されるURLが変わらないままで、`/test1/index.html`のページを表示させてください

### PH3-3 Virtual Host
下記の要件で、設定してください
* [http://nxxxl-test.com/test/](http://nxxxl-test.com/test/)  
 * `/test1/index.html`を表示させてください
* [http://nxxxl-test2.com/test/](http://nxxxl-test2.com/test/)
 * `/test2/index.html`を表示させてください
 * [http://www.nxxxl-test2.com/test/](http://www.nxxxl-test2.com/test/)も同じページを表示させてください。（ブラウザにて表示されるURLの変更はOK)
 * アクセスパスワードをかけてください

### PH3-4 HTTPS
* [https://nxxxl-test2.com/test/](https://nxxxl-test.com/test/) へのアクセスを可能にしてください

### PH3-5 アクセス制御
|No|パス|要件|
|:-----|:--------|:-----------|
| 1  | http://nxxxl-test.com/  | 1.誰でもアクセス可能  |
| 2   | http://nxxxl-test.com/about/  |  1.Basic認証：下記のユーザーのみアクセス可能 </br> `root:123456` </br> `guest:guest`  <br> 2. URL書き換えて、`http://nxxxl-test2.com/about/` へリダイレクト|
| 3   | http://nxxxl-test.com/secret/   | 1. localhostのみアクセス可能 <br> 2.localhost以外アクセス不可  |
| 4   | https://nxxxl-test2.com/test/  |  1.Basic認証：下記のユーザーのみアクセス可能 </br> `root:123456` |
| 5   | http://nxxxl-test.com/youshallnotpass/  | 1.誰でもアクセス禁止  |

### PH3-6 HTTPヘッダー制御
3-5に加え、下記の要件を満たして設定する  

|No|パス|要件|
|:-----|:--------|:-----------|
| 1   |  http://nxxxl-test2.com/about/ | 1. `http://nxxxl-test.com/about/` から遷移した場合のみアクセス可能  |
| 2   | http://nxxxl-test2.com/owner/  |  1. Chromeブラウザでアクセスする場合アクセス可能 <br> 備考：MacのSafari最新版からアクセスする時、禁止されればOK |


## 【WIP】 技術課題PH4
### PH4習得目標
* CSSの基本知識
* CSSクラスの定義方法
* CSS利用で開発するメリット
* JSの基本知識
* DOMの概念
* イベントの概念
* `Ajax`通信の基礎
* JQueryの基本知識
* JQuery Selectorの基本知識
* (非必須) 他のJSフレームワーク：BootStrap
* (非必須) 他のJSフレームワーク：Vue.js

### PH4-0 下記のサイトをさらっと目を通してください
* [CSSチュートリアル](http://www.w3big.com/ja/css/default.html)
* [JSチュートリアル](http://www.w3big.com/ja/js/default.html)
* [JQueryチュートリアル](http://www.w3big.com/ja/jquery/default.html)

### PH4-1下記のページを真似して作成してください
[Problem 1](https://snowdays.world/problem/Problem1.html)
### PH4-2下記のページを真似して作成してください
[Problem 2](https://snowdays.world/problem/Problem2.html)
#### 備考
* Youtubeの制限により、IPから始まるURL(`localhost`や`http:xx.xx.xx.xx`など)からYoutubeにあるコンテンツをリクエストする時、「このコンテンツの再生が制限されている」という旨のメッセージが表示される可能性あり。そこできちんとドメイン名が付いているURLでテストしたほうがいい(`http://nxxxl-test2.com/problem/Problem2.html`)
* はなるべくObjectで作成してみてください
```
function MusicItem(singer, title, genre, embedCode) {
      return {
        singer: singer,
        title: title,
        genre: genre,
        embedCode: embedCode
      }
    }
```
* 難易度かなり高いと思うが、きちんと勉強できることが多い為、あえてJSを難読化した

### 【WIP】 PH4-3下記のページを真似して作成してください

## 【WIP】 技術課題PH5
### 【WIP】 PH5習得目標
* HTTP、HTTPSの通信仕組み
* リモートAPIのコール
* 正規表現

### 【WIP】 PH5-1 下記のサーバーステータス監視仕組みを作成してください
### 【WIP】 PH5-2 SLACKの通知仕組みを作成してください
### 【WIP】 PH5-3 URLの監視仕組みをアクセスしてください
