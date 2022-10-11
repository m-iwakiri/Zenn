---
title: "【Web制作実践】LPを制作してみる Part2 LPの大枠をコーディング"
emoji: "🤖"
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
Part2 では、ワイヤーフレームやデザインをもとに実際にコーディングの工程に入っていきます。
:::

# 全体のイメージを把握

LPの狙いやコンセプトを決め、デザインが完成したらいよいよコーディングの工程に移っていきます。

今回は既存のLPを模写する形で進めるので、以下の画像のようなデザインを受け取ったとします。
＊とあるスクールの募集用LPです。

:::message alert
なお、すべてそのまま表示するとページが非常に長くなってしまうため、載せているのはLPの最上部だけです。
全体は画像をクリックすると表示できるようにしてます。
また、実際のサービス名やテキストの部分は伏せる形で掲載しています。
:::

-----
[![](/images/web_practice_lp/lp-design-pc-thumb.jpg)](https://zenn.office-iwakiri.com/articles/web_practice_lp/lp-design-pc01.png)
*PC向けのデザイン*

-----
[![](/images/web_practice_lp/lp-design-sp-thumb.jpg)](https://zenn.office-iwakiri.com/articles/web_practice_lp/lp-design-sp01.png)
*スマホ向けのデザイン*

-----

この段階で、同時にワイヤーフレームもあれば、LP全体の構成もイメージしやすいと思いますが、プロジェクトによってはワイヤーフレームを作っていない場合もありますので、デザインをもとに全体の構成もイメージできるようにしておいた方が良いです。

今回のLPの場合、デザインをもとにLP全体の構成を明らかにしていくと、以下のような構成になるかと思います。

- ヘッダー
  * ロゴ
  * ナビゲーションメニュー(PCのみ)
  * 問い合わせボタン(PCのみ)
  * メニュー開閉ボタン(スマホのみ)
- LPのメインコンテンツ
    - ファーストビュー
        * ファーストビュー画像
        * キャッチコピー
    - 対談動画
    - こんな人におすすめです
    - 診断結果動画
    - コンテンツ枠１
    - お申し込みはこちら
    - 講師紹介
    - お申し込みはこちら
    - バナー枠
    - 当講座のサポート内容
    - お申し込みはこちら
    - 注意事項・事前準備
    - お申し込みはこちら
    - よくあるご質問
- フッター
  * お問い合わせ
  * ナビゲーションメニュー
  * 上に戻るボタン
  * SNSリンク
  * コピーライト表記

あえて省略せずにすべてピックアップしたので、項目が非常に多くなっていますが、LPの場合は1ページに盛り込む情報量も多くなりがちなので、こればかりは仕方ありません。

これだけ見ると非常に大変に思えてしまうのですが、このように箇条書きで洗い出すのは非常に大事なステップで、この箇条書きの項目がページ内での「内容的な区切り」になってきますので、この「内容的な区切り」を意識してコーディングを行うのが非常に重要なのです。

また、デザインの傾向としては「内容的な区切り」毎にデザインを変えてみたり、交互に同じようなデザインが登場したり、といったことも良く行われますし、区切りのタイミングで「お問い合わせはこちら」の枠が登場してくる場合もあります。
＊今回のLPの場合は、「内容的な区切り」毎に「お申し込みはこちら」が登場するパターン

実際にコーディングに入る際、基本的にはHTMLファイルは単純なテキストファイルなので、上から順に書いていくことが多いですが、いきなりデザインの上の方からコーディングを始めてしまうと、全体が見えていない状態でコーディングに入ってしまうことになります。
全体が見えていない状態でコーディングを始めてしまうと、ページの内容的な構成をあまり踏まえないコーディングになってしまったり、同じパターンが繰り返しで登場して再利用できるにもかかわらず、再利用が出来ずにコーディングの効率が悪くなったり、といったことが起こりますので、最初に全体を見渡すことは非常に重要になってきます。

# LPの大枠からコーディング

デザインをもとに、LP全体の「内容的な区切り」がイメージできたら、実際のコーディング作業に入っていきます。

コーディングのスタイルは人それぞれかとは思いますが、全体の大きな枠組み、内容的な区切りをまず最初にコーディングするのが個人的には効率が良くておススメです。

実際の建造物なんかをイメージしていただくと分かりやすいと思いますが、建物もまずは基礎の土台部分を作って、骨組みを組み立てて、とやっていきますが、HTMLのコーディングにおいても、それと同じアプローチが出来るのです。

では、実際に例示したデザインをもとに、LPの大枠をコーディングしたものがこちらです。

```html
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
            <section id="ruby_aws"></section>
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

これだけコーディングしても、ブラウザには何も表示されず白紙のページしか表示されませんが、最初はそれでOKです。

最初の段階で、大枠をしっかりと組み立てておくというのが非常に大事で、なおかつ、各区切りごとに`class`や`id`に適切な名称を振れればなおOKです。

基本的にLPをコーディングする際には、HTMLだけをコーディングするわけではなく、CSSやJavaScriptのコーディングも必要になってきます。
CSSにせよ、JavaScriptにせよ、HTMLの構造に依存する部分も大きいので、HTMLの枠組みがあいまいな状態で進めて後で枠組みを見直すような事態になってしまうと、文章の構造を変えたことでCSSやJavaScriptにも修正が発生する事態になってしまいます。

そういった手戻りのリスクを避ける為にも構造を固めておくのは非常に大事ですし、「内容的な区切り」毎にHTML/CSS/JavaScriptを並行してコーディングしていくようなスタイルで進めていく場合も先に大枠を固めておく方が作業が進めやすくなります。


ということで、Part2はここまで。

