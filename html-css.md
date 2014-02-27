# HTML + CSSコーディング規約

ここではWebアプリケーション開発のHTML及びCSSのコーディング規約を示します。基本的にはGoogleの[コーディング規約](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)に準拠するような形で作成されています。

## 書式ルール

### インデント

インデントには半角スペース2つ分でインデントします。タブコードやタブコードとスペースを混在させるのは禁止です。

```html
<ul>
  <li>Fantastic
  <li>Great
</ul>
```

### 大文字 / 小文字

すべて小文字を使用してください。

```html
<!-- NG -->
<A HREF="/">Home</A>

<!-- OK -->
<img src="google.png" alt="Google">
```

### 文末のスペース

文末のスペースを削除する。

```html
<!-- NG -->
<p>What?_

<!-- OK -->
<p>Yes please.
```

## 全般的なメタルール

### エンコード

エンコードは、UTF-8（BOM無し）を使用してください。以下をHTMLファイルに記述してエンコードを指定します。

```html
<meta charset="utf-8">
```

## HTMLのスタイルルール

### ドキュメントタイプ

HTML5を使用してください。以下で始まる形式で書きます。

```html
<!DOCTYPE html>
```

### HTMLのバリデート

可能な限り適切なHTMLを記述してください。[HTML valid](http://validator.w3.org/nu/)などを使用しながら確認をしてください。

### セマンティックに書く

目的に応じてHTMLを記述してください。見出しならhx要素、段落ならp要素、アンカーならa要素など目的に応じたHTML要素を使ってください。

リンクならa要素で書いてください。onclickのようなJavaScriptな振る舞いのものを要素の属性に入れないでください。

```html
<!-- NG -->
<div onclick="goToRecommendations();">All recommendations</div>

<!-- OK -->
<a href="recommendations/">All recommendations</a>
```

### マルチメディアの代替コンテンツ

マルチメディアの要素には、代替コンテンツを提供してください。画像には、意味のある代替テキストをalt属性として、動画・オーディオコンテンツにはキャプションを記述してください。

装飾的な用途の場合など意味を持たない画像については、代替テキストは記述せずにalt=“"としてください。

```html
<!-- NG -->
<img src="spreadsheet.png">

<!-- OK -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

### 構成要素の分離

文書構造・見た目・振る舞いは、分離してください。見た目に関するものはスタイルシートに、振る舞いに関するものはスクリプトへ移して記述してください。

```html
<!-- NG -->
<!DOCTYPE html>
<title>HTML sucks</title>
<link rel="stylesheet" href="base.css" media="screen">
<link rel="stylesheet" href="grid.css" media="screen">
<link rel="stylesheet" href="print.css" media="print">
<h1 style="font-size: 1em;">HTML sucks</h1>
<p>I’ve read about this on a few sites but now I’m sure:
  <u>HTML is stupid!!1</u>
<center>I can’t believe there’s no way to control the styling of
  my website without doing everything all over again!</center>

<!-- OK -->
<!DOCTYPE html>
<title>My first CSS-only redesign</title>
<link rel="stylesheet" href="default.css">
<h1>My first CSS-only redesign</h1>
<p>I’ve read about this on a few sites but today I’m actually
  doing it: separating concerns and avoiding anything in the HTML of
  my website that is presentational.
<p>It’s awesome!
```

### 実体参照

不要な実体参照は使用しないでください。UTF-8においては、—（&mdash;）・”（&rdquo;）・☺（&#x263a;）のような文字は実体参照を使う必要はないです。HTMLで特別な意味を持つ文字（ < や & など）は例外です。

```html
<!-- NG -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.

<!-- OK -->
The currency symbol for the Euro is “€”.
```

### タグの省略

省略できるタグは、省略してもかまいません。ファイルサイズの最適化が図れます。ただし、省略する場合は、省略をルールとして統一してください。

### type属性

CSSとJavaScriptのtype属性は省略してください。HTML5ではデフォルトの言語として解釈されるためです。

```html
<!-- NG -->
<link rel="stylesheet" href="//www.google.com/css/maia.css" type="text/css">

<!-- OK -->
<link rel="stylesheet" href="//www.google.com/css/maia.css">
```

```html
<!-- NG -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>

<!-- OK -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
```

## HTMLの書式ルール

### 全般的な書式

ブロック要素・リスト要素・テーブル要素は改行してから記述し、それらの子要素にはインデントを入いれてください。横並びリストなど改行による空白が問題になる場合は、li要素をすべて一行で書いても大丈夫です。

```html
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>

<ul>
  <li>Moe
  <li>Larry
  <li>Curly
</ul>

<table>
  <thead>
    <tr>
      <th scope="col">Income
      <th scope="col">Taxes
  <tbody>
    <tr>
      <td>$ 5.00
      <td>$ 4.50
</table>
```

## CSSスタイルルール

### CSSのバリデート

可能な限り適切なCSSを記述してください。CSSバリデーターにバグがある場合や独自の構文を必要としない限りは、ちゃんと書いてください。HTML同様[W3C CSS validator](http://jigsaw.w3.org/css-validator/)などのツールで検証してください。

### IDとクラスの命名

IDとクラス名にはちゃんと意味の分かる名前を使ってください。見た目を反映したものやそれが何を表しているか不可解な名前ではなく、要素の目的や役割を反映した名前を付けてください。

```css
/* NG: 意味がわからない */
#yee-1901 {}

/* NG: 見た目を表してる */
.button-green {}
.clear {}

/* OK: 役割を表してる */
#gallery {}
#login {}
.video {}

/* OK: 汎用的な名前 */
.aux {}
.alt {}
```

### IDとクラスの命名スタイル

意味の分かる範囲でできるだけ短いIDとクラス名を使ってください。短くしすぎて意味がわからなくなるようなのはNGです。

```css
/* NG */
#navigation {}
.atr {}

/* OK */
#nav {}
.author {}
```

### タイプセレクタの記述

IDとクラス名にタイプセレクタは記述しないでください。パフォーマンスを考慮して不要な子孫セレクタも避けましょう。

```css
/* NG */
ul#example {}
div.error {}

/* OK */
#example {}
.error {}
```

### ショートハンドプロパティ

可能な限りショートハンドでプロパティを書いてください。

```css
/* NG */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;

/* OK */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```

### 「0」と単位

値が「0」なら単位を省略してください。

```css
margin: 0;
padding: 0;
```

### 小数点の頭の「0」

小数点の頭の「0」は省略してください。

```css
font-size: .8em;
```

### URI値の引用符

url()での指定において、”“（ダブルコーテーション）や'‘（シングルコーテーション）などのURI値の引用符を省略してください。

```css
@import url(//www.google.com/css/go.css);
```

### HEX形式のカラーコード

HEX形式のカラーコードで3文字で表記できるものは3文字にしてください。

```css
/* NG */
color: #eebbcc;

/* OK */
color: #ebc;
```

### プレフィックス（接頭辞）

IDやクラス名が重複しそうな大規模プロジェクトの場合、IDやクラス名には固有の接頭辞を付けてかまいません。接頭辞は後ろにハイフンを付けて繋げます。

```css
.adw-help {} /* AdWords */
#maia-note {} /* Maia */
```

### IDやクラス名の区切り文字

IDやクラス名の別々の単語はハイフンで繋いでください。

```css
/* NG: [demo]と[image]が繋がってる */
.demoimage {}

/* NG: アンダーバーで繋がってる */
.error_status {}

/* OK */
#video-id {}
.ads-sample {}
```

### CSSハック

ユーザーエージェント別の対応のためにCSSハックを使う前に別の方法を試してください。CSSハックは、ユーザーエージェントごとの違いを吸収するためには簡単で魅力的な方法ですが、プロジェクト全体のコードの品質を落とすことにもなるので「最後の手段」として考えてください。

## CSS書式ルール

### ブロック単位のインデント

その階層がわかるようにブロック単位でコードをインデントしてください。

```css
@media screen, projection {
  html {
    background: #fff;
    color: #444;
  }
}
```

### プロパティの終端

すべてのプロパティの終端はセミコロンを書いてください。

```css
/* NG */
.test {
  display: block;
  height: 100px
}

/* OK */
.test {
  display: block;
  height: 100px;
}
```

### プロパティ名の終端

すべてのプロパティ名の終端にはコロンの後にスペースを入れてください。

```css
/* NG */
h3 {
  font-weight:bold;
}

/* OK */
h3 {
  font-weight: bold;
}
```

### セレクタとプロパティの分離

別々のセレクタとプロパティは改行して書いてください。

```css
/* NG */
a:focus, a:active {
  position: relative; top: 1px;
}

/* OK */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```

### CSSルールの分離

別々のCSSルールは改行して一行間を空けて書いてください。

```css
html {
  background: #fff;
}

body {
  margin: auto;
  width: 50%;
}
```

