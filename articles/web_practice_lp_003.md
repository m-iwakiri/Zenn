---
title: "【Web制作実践】LPを制作してみる Part3 各種メタ情報のコーディング"
emoji: "😽"
type: "tech" # tech: 技術記事 / idea: アイデア
topics:
    - "HTML"
    - "CSS"
    - "LP"
published: false
---
:::message
この記事はHTML/CSSを勉強中の方向けにLPの制作過程を追いながら、コーディング上のポイントなどを解説する記事です。
既存のLPを模写しながら、LPの制作過程を追っていく、という流れになります。
:::

:::message
Part3 では、Webページ上には直接表示されないものの、検索サイトからの流入などを考えた場合に必須となる各種の『メタ情報』をコーディングします。
:::

# 前回コーディングした内容

前回はページの大枠のコーディングということで、以下の状態になっているかと思います。
今回はこの続きでやって行きます。

```html:lp.html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LPのタイトル</title>
</head>
<body>
    <header>
        <div class="logo"></div>
        <nav></nav>
        <div id="menu_open"></div>
    </header>
    <main id="main_wrapper">
        <article>
            <section id="fv"></section>
            <section id="movie"></section>
            <section id="recommend"></section>
            <section id="diagnostics"></section>
            <section id="contents1"></section>
            <section class="cta"></section>
            <section id="teacher"></section>
            <section class="cta"></section>
            <section id="price"></section>
            <section id="supoprt"></section>
            <section class="cta"></section>
            <section id="notice"></section>
            <section class="cta"></section>
            <section id="faq"></section>
        </article>
    </main>
    <footer>
        <div class="contact"></div>
        <nav></nav>
        <div class="go_top"></div>
        <div class="sns"></div>
        <div class="copyright"></div>
    </footer>
</body>
</html>
```

# メタ情報とは

LP（Webページ）における「メタ情報」とは、LPに直接表示されるコンテンツではないものの、LPに付随して付け加えられるさまざまな情報のことを指します。
主なものとして、以下のような情報があります。

- ページのタイトル（表題）
- ページの内容を簡潔にまとめた概要テキスト
- ページで扱っている主なキーワード
- 各種SNSでシェアする際に使用される情報

# メタ情報のコーディング
## DOCTYPE宣言

これはメタ情報ではないですが、Webページには必須の記述なので紹介しておきます。
基本的には、HTMLの最初の行に以下のように記載します。

```html
<!DOCTYPE html>
```

これから作るWebページであれば、このシンプルな記述でOKですが、比較的古いサイトだとこの部分がもっと複雑な記述になっていました。

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```
＊HTML4.01 Strict DTD（厳密型DTD）の場合

実はHTMLの規格自体はずっと同じというわけではなく、バージョンアップを繰り返しています。
その流れの中で、最新の「HTML5」という規格では、例示したようなシンプルな記述で良くなった、ということです。

## <html>タグ

基本的にWebページ（HTML文書）では、「HTMLタグ」というものを使ってページを記述していくのですが、そのHTMLタグで「入れ子」という構造を作って、文書の構造を組み立てていく形になっています。
現時点でも、すでに複数のタグが入れ子になった状態になっていますが、タグを入れ子にして構造を組み立てていくので、「文書の大枠からまずは組み立てる」といった作り方ができるのです。

で、このHTML文書の「一番大元」になるタグが`<html>`タグということになります。
これがあることで、ブラウザはその文書が`<html>`タグの部分から始まり、`</html>`閉じタグまでの範囲がWebページだと認識してくれるようになっています。

なお、今回の例では以下のように記述されています。

```html
<!DOCTYPE html>
<html lang="ja">
  （中略）
</html>
```

この`lang="ja"`の記述ですが、このようにHTMLのタグの内部に書かれる情報のことを「属性」と呼び、タグに対してなんらかの追加情報を与える際に使います。

今回の場合は、`<html>`タグ内に`lang="ja"`という「lang属性」を記述することで、このWebページが「日本語」で記述されていることを表しています。

最近のブラウザだと「翻訳機能」がついていたりしますが、ブラウザで自動翻訳機能を使う際に「lang属性」を元にして翻訳されるようになっていますので、ここを適当にしていると、意図せず自動翻訳でメチャクチャな文書になってしまうことがあるので正しく設定しましょう。

## <head>タグ

各種のメタ情報はこの`<head>`タグ〜`</head>`閉じタグの間に記述します。
基本的にこの`<head>`タグ内に記述された内容は、Webページの内容としては表示されませんので、この場所に画面上には表示しない「メタ情報」を書いていくという流れになります。

### <title>タグ

`<title>`タグはそのWebページの「表題」を記載するためのタグとなっており、`<title>`タグと`</title>`閉じタグの間に記述されたテキストがブラウザの「タブ」のタイトルとして表示されます。
また、Googleなどの検索結果にもページのタイトルとしてこのテキストが表示されるようになっています。
文字種や文字数に具体的な制限があるわけではありませんが、あまり長いとテキストを最後まで表示してくれないため、できるだけ簡潔で分かりやすいタイトルを付けるようにしましょう。
＊日本語では30文字前後までが望ましいと言われています。

### <meta>タグ

`<title>`タグは`<title`タグや`<link>`タグでは表せない、任意のメタ情報を記述するためのタグとなっており、`name属性`などを組み合わせて使うことで、意味を持たせたメタ情報を記述できるようになっています。

指定できる属性は先述の`name属性`以外に、`charset属性`、`http-equiv属性`、`content属性`があります。
それぞれどのように使うかは、具体的な事例の中で紹介して行きます。

1. ページの文字コード（文字エンコーディング）

```html:記述例
<head>
  <meta charset="UTF-8">
</head>
```

このように書くことで、そのWebページは「UTF-8」という文字コードで記述されている、という意味になります。
これは、ブラウザでページを表示する際に非常に重要な情報で、基本的にそのファイルを保存したときの文字コードと同じものを記載することになっています。
そこに不整合があると「文字化け」を起こしてページが正常に表示されない場合があります。

2. 古いブラウザへの対応

```html:記述例
<head>
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
</head>
```

これは、今から新規でLPを作成するのであれば、記述しなくても良いかもしれませんが、Visual Studio Codeなどのテキストエディタで補完機能を使って入力しているときに自動的にこの記述が挿入されることが多いです。

この記述は2022年6月にサポートが終了した「Internet Explorer」（以下IE）というMicrosoftの古いブラウザーに対応するための記述で、この例では「インストールされているIEの中で最新のバージョンを使って表示してください」という意味の記述になります。

サイトの方針でIEもサポートする、というのでなければ必要のない記述ですが、あっても特に不具合は起きませんので、あえて記述する必要はないけれど、自動補完された記述を消す必要まではない、という認識でOKです。

3. スマートフォンやタブレットなどへの対応（viewportの設定）

```html:記述例
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

最近のWebサイトは「レスポンシブデザイン」ということで、PCでもスマートフォンでも閲覧できるようなデザインになっていることが多いですが、その際に必須になるのがこの記述です。
