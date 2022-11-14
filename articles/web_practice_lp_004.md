---
title: "【Web制作実践】LPを制作してみる Part4 固定ヘッダーのコーディング"
emoji: "👏"
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
Part4 では、ページ最上部のヘッダー部分をコーディングします。
:::

# 完了時の見本

Part4の作業まで行うと、ページの最上部に下図のようなヘッダーが表示され、画面をスクロールしても常時表示されるようになります。

なお、PCとスマートフォンで表示する内容も変えています。（ブレイクポイントは768pxとしています）

## PC版のヘッダー
![](/images/web_practice_lp/lp-design-pc02.png)

ロゴと他のページへのリンクが横方向に並んで配置されています。


## スマホ版のヘッダー
![](/images/web_practice_lp/lp-design-sp02.png)

他のページへのリンクをなくす代わりに、右側にメニューボタンを配置してそこをタップするとメニューが開くようにしています。

# ヘッダーのブロック部分をコーディング

## HTMLコーディング

今回のLPのヘッダーにはロゴや他のページへのリンクが表示されていますが、その部分の背景がPCでは半透明の白、スマホでは白背景となっており、ページの全幅にわたって表示されています。
また、PC表示の場合はヘッダーの中身の部分が最大でも1200pxになるようにしていきます。（あまり左右に広げすぎると間延びした印象になるため）

それを踏まえて、下記のようにHTMLをコーディングしていきます。

```html
<body>
  <header id="header">
    <div class="header_inner">
      <div class="logo"></div>
      <nav class="pc_navi"></nav>
      <div id="menu_open"></div>
    </div>
  </header>
</body>
```

## CSSファイルとの関連付け

HTMLをコーディングしただけでは、デザインは何も施されていない状態ですので、デザインについてはCSSでコーディングしていきます。
その際、HTMLとCSSを関連付けるために、HTML側に記述を追加する必要があります。

```html
<!DOCTYPE html>
<html lang="ja">
<head>
（略）
  <link rel="stylesheet" href="https://unpkg.com/ress/dist/ress.min.css" />
  <link rel="stylesheet" href="sample.css" />
</head>
```

このように`<link>`タグを記述し、`rel`属性については`rel="stylesheet"`で固定。`href`属性でCSSファイルへのパス/URLを記述するのが基本です。

1つ目のCSSは「リセットCSS」というもので、ブラウザのデフォルト値で表示されるのを回避するためによく使われるものです。
2つ目のCSSはそのページ固有のCSSとなります。

この例のように、必要であれば複数のCSSファイルを記述することも可能ですが、記載する順番も非常に重要で、外部のライブラリであったり、サイト全体で共通で使うようなCSSを先に記述するのが一般的です。

詳細なルールはここでは解説しませんが、指定が重複した場合に「後出し優先」になるのがCSSの基本になるので、ページ固有のCSSを後に記述する、という点を押さえておいてください。

そのうえで、CSSのコーディングを行っていきます。

### ヘッダーを固定する

```css:sample.css
body{
  background-color: #cccccc;
  height: 200vh;
}
#header{
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100;
  width: 100%;
  background-color: #ffffff;
}
#header .header_inner {
  padding: 20px 15px;
}

@media (min-width: 768px){
  #header {
    background-color: rgba(255, 255, 255, 0.8);
  }
  #header .header_inner {
    padding: 45px 15px;
    margin: 0 auto;
    max-width: 1230px;
  }
}
```

まず、`body`タグへの指定ですが、`background-color: #cccccc;`で背景色を薄めのグレーに、`height: 200vh;`で高さをウィンドウの高さの2倍にしていますが、これはヘッダーとの見分けが付くように、かつ画面がスクロール出来るようにするための動作確認用の記述です。

今回はヘッダーの外枠部分に`id="header"`とIDを指定しています。
その`#header`に対して、`position: fixed;`と指定することで、ウィンドウ内での位置を固定にしています。固定にした場合は、座標位置を指定しないといけないので、`top: 0;`でウィンドウの上端、`left: 0;`でウィンドウの左端をそれぞれ指定しています。
また、前後の重なり順も意識しないといけないので、`z-index: 100;`も併せて指定しています。

その上で、ヘッダーを画面幅いっぱいに広げたいため、`width: 100%;`を指定し、`background`プロパティで背景色を指定します。
今回はPC版の場合に背景色を半透明にしたいので、『メディアクエリ』を使用し、画面幅が768px以上の場合にPC向けのデザインに切り替わるようにしています。
`@media (min-width: 768px){ ~ }`の部分がそれに該当します。


### ヘッダーの内側ブロック
```css:sample.css
#header .header_inner {
  padding: 20px 15px;
}
@media (min-width: 768px){
  #header .header_inner {
    padding: 45px 15px;
    margin: 0 auto;
    max-width: 1230px;
  }
}
```

ヘッダーの内側ブロックには、`class="header_inner"`とクラス名を指定しています。
今回は、その内側に対してパディングを設定しています。
また、PC版の場合、内側ブロックを最大でも1200pxまでで納めたいので、`max-width: 1230px;`としています。（左右パディング分を加えて1230px）


### ヘッダーの中身をコーディング

```html
<body>
  <header id="header">
    <div class="header_inner">
      <div class="logo">
        <h1><img src="./images/logo.png" alt="ロゴの代替テキスト" /></h1>
      </div>
      <nav class="pc_navi">
        <ul>
          <li><a href="#">ホーム</a></li>
          <li><a href="#">サービス案内</a></li>
          <li><a href="#">オンライン講座</a></li>
          <li><a href="#">会社概要</a></li>
          <li><a href="#">お問合せ</a></li>
          <li><a href="#">ブログ</a></li>
        </ul>
        <a href="#" id="contact">お問い合わせはこちら</a>
      </nav>
      <a id="menu_open"><span></span><span></span><span></span></a>
    </div>
  </header>
</body>
```

ロゴを表示する部分は`logo`クラスとし、「ホーム」～「お問い合わせはこちら」のリンク部分はPC版のみ表示なので、`<nav>`タグでまとめ`pc_navi`クラスとしました。
また、スマホ版でのみ表示するメニュー開閉ボタンもIDを`menu_open`として用意しています。`#menu_open`内の`<span>`タグはよく見かける3本線のメニューボタンのデザインを実現するために配置しています。この方法なら画像やWebフォントを使わずに実現できます。