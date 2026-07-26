---
title: ひらがなとカタカナを学ぶページ
date: 2026-07-24 09:57:10 +0100
categories: [Coding, WebDev, Projects]
tags:
  - WebDev
  - Spanish
  - Projects

excerpt: この投稿では、私が開発したプロジェクトの一つについて紹介します。これは、日本語のひらがなやカタカナを復習したり学んだりできるサイトです。

toc: true
toc_sticky: true
use_math: true

language: jp
ref: japanese-learning-website
lang_en: /en/japanese-learning-website
lang_es: /es/japanese-learning-website
lang_ja: /jp/japanese-learning-website
permalink: /jp/japanese-learning-website

header:
  overlay_image: /assets/images/japanese-learning-website/teaser-image.png
  overlay_filter: 0.25
  teaser: /assets/images/japanese-learning-website/teaser-image.png
---

現在も日本語を勉強中ですので、この投稿では翻訳ツールを利用しました。もし誤りを見つけた場合は、修正のためご連絡ください。よろしくお願いします。
{: .notice--danger }

# 目的

これは、以前ひらがなやカタカナの練習に使っていたサイトがなくなってしまったため、やむを得ず作成したプロジェクトです。そこで、自分なりに似たようなサイトを作り、使えるようにしました。かなりシンプルなものではありますが、面白いプロジェクトだったと思います。

## コード

ソースコードはGitHubで公開されており、ひらがな版は[こちら](https://github.com/oviwanazul124/HiraganaPractice)、カタカナ版は[こちら](https://github.com/oviwanazul124/KanaPractice)からアクセスできます。

### HTML

まずHTMLコードから見ていくと、これは2つの[JavaScript](#javascript)ファイルと連動しているフォームです。まずは、フォームで使用されているコードを確認してみましょう。

```html
<div class="answerZone">
  <h2 id="kana">ア</h2>
  <p id="feedbackText"></p>
  <input type="text" id="inputKana" />
  <br />
  <button id="kanaSettingsTitle">Kana Settings (Click to Toggle)</button>
</div>

<!-- コードの続き... -->
```

ご覧の通り、このディバイダーには回答エリアが含まれており、そこには**H2**要素があります。これは[JavaScript](#javascript)のコードによって、カタカナの「あ」をプレースホルダーとして使用して変更されます。その後に、**feedbackText**という名前の段落があり、ユーザーが入力した読みが正しいかどうかを表示する役割を担っています。さらに、回答エリアもあります。さらに、どの文字を表示するかを設定できるオプションもあります。

ひらがな版のコードを見てみると、一部のIDは変わっていますが、その背後にあるロジックは同じであることがわかります。
{: .notice--info}

下の写真には、完成した様子が写っています。

![Photo-Answer](/assets/images/japanese-learning-website/teaser-image.png)

ここでは、カタカナの設定におけるHTMLセクションについて説明します。この設定はグループで構成されており、主要な母音がグループ分けされています。この例では、コードの説明のために母音**A**に焦点を当てます。

コードはすべてのグループで同じように繰り返されるので、1つ説明すれば十分です
{: .notice--info}

```html
<div id="kanaSettings" class="SettingsZone">
  <div id="kanaContent">
    <h5 id="kanaTitle">A</h5>
    <hr />
    <label><input type="checkbox" id="mARow" checked /> Select all </label>
    <br />
    <label><input type="checkbox" id="aRow" value="a" checked />ア</label>
    <!-- 残りの文字に関するコードの続き -->
  </div>
</div>
```

ご覧の通り、設定用のメインディバイダーと、カタカナの内容用のディバイダーがそれぞれ用意されています。その後、各母音の値には「h5」が割り当てられており、どの母音の値を設定するかを示しています。また、2種類のボタンがあります。1つは1回だけ表示される「すべて選択」ボタンで、その名の通り、学習対象となるすべての音が選択されるようにする役割を担っています。一方、ボタンが存在する数だけ繰り返し表示されるもう1つのボタンは「個別の音」ボタンです。両者は多くの類似点がありますが、「個別の音」ボタンには**value**という値も含まれています。これについては、後ほど[JavaScript](#javascript)のコード解説で重要になります。

![Photo-Settings](/assets/images/japanese-learning-website/settings.png)

### JavaScript

まず最初に、2つのJavaScriptファイルがあります。1つ目は**main.js**、2つ目は**globalcheckbox.js**というファイルで、まずはmain.jsから始めましょう。

#### main.js

Main.jsは、その名前が示す通り、問題のランダム生成と回答の検証を主に担当します。最初に目にするのは辞書で、この辞書は回答を定義し、選択された文字と正しい回答を関連付けています。これはコードの例からも確認できます。

```javascript
const kana = [
  { kana: "ア", romanji: "a" },
  /* コードは各文字ごとに続きます */
];
```

これで、質問を表示するための画面、ユーザーからの情報を入力するための入力欄、フィードバックテキスト用の段落、解答確認ボタン、そして最後に現在の問題を管理するための変数が用意されました。

```javascript
/* コードは上記に続く */

const kanaDisplay = document.getElementById("kana");
const inputKana = document.getElementById("inputKana");
const feedbackText = document.getElementById("feedbackText");
const sumbitBtn = document.getElementById("sumbit");

let currentItem = null;

/* コードは上記に続く */
```

これで、[nextKana()](#nextkana) と [checkKana()](#checkkana) の両方の関数が定義されました。続いて、ボタンの動作を変更するためのコードが以下のように記述されています。これにより、ブラウザでEnterキーを押すと、デフォルトのアクションが解除され、代わりに [checkKana()](#checkkana) 関数が実行されるようになります。

```javascript
if (event.key === "Enter") {
  event.preventDefault();
  checkKana();
}
```

最後に、設定画面を開閉するためのコードを紹介します。これを行うには、設定画面のタイトルと内容を取得し、タイトルがクリックされた際のイベントにリスナーを追加します。これにより、デフォルトの動作を差し止め、表示状態を反転させます（つまり、表示されている場合は非表示に、非表示の場合は表示に切り替えます）。

```javascript
/* コードは上記に続く */

const kanaSettingsTitle = document.getElementById("kanaSettingsTitle");
const kanaContentSettings = document.getElementById("kanaSettings");

kanaSettingsTitle.addEventListener("click", function () {
  event.preventDefault();
  kanaContentSettings.hidden = !kanaContentSettings.hidden;
});
```

##### nextKana()

この関数は、ページに表示され、推測されることになる次の文字を生成する役割を担っています。

```javascript
function nextKana() {
  const selectedKana = document.querySelectorAll(
    '#kanaSettings input[type="checkbox"]:checked',
  );

  const activeKanaValues = Array.from(selectedKana).map((box) => box.value);

  if (activeKanaValues.length == 0) {
    feedbackText.textContent = "Please select at least one";
    return;
  }

  /* コードはここから続きます */
}
```

ご覧の通り、この関数はまず、調査対象として選択した値を取得し、それらを定数**selectedKana**に格納します。その後、その定数に基づいてマッピングを行い、どの値がアクティブであるかを確認します。万が一、ユーザーがフィードバックテキストで「0」を選択した場合、**Please select at least one**というメッセージが表示されます。

```javascript
function nextKana() {
  /* 上で見てきたコード */

  const activeKana = kana.filter((item) =>
    activeKanaValues.includes(item.romanji),
  );

  const randomIndex = Math.floor(Math.random() * activeKana.length);

  currentItem = activeKana[randomIndex];

  kanaDisplay.textContent = currentItem.kana;

  inputKana.value = "";

  feedbackText.textContent = "";
}
```

続いて、このコードは、アクティブなアイテムからその回答をローマ字で取得して保存し、ユーザーに表示する文字をランダムに選択するために使用するランダムなインデックスを生成します。これを変数**currentItem**に保存した後、回答の内容を表示し、回答とフィードバックの両方をリセットします。

#### checkKana()

次に、**checkKana()**という関数を分析してみましょう。この関数はまず、現在のアイテムが存在するかどうかを確認し、存在しない場合は空を返します。その後、ユーザーが入力した大文字を含まない文字列を取得して、変数**kanaUser**に格納します。続いて、回答が正しいかどうかを確認し、ユーザーにフィードバックを提供します。

```javascript
function checkKana() {
  if (!currentItem) return;

  const kanaUser = inputKana.value.toLowerCase();

  if (kanaUser == currentItem.romanji) {
    setTimeout(nextKana, 750);
    feedbackText.textContent = "Correct";
  } else {
    setTimeout(nextKana, 750);
    feedbackText.textContent =
      "Incorrect. The writing is " + currentItem.romanji;
  }
}
```

## リンクとGitHub。

このプロジェクトは、それぞれのウェブサイトから直接アクセスできます。カタカナ版は [Katakana](https://oviwanazul124.github.io/KanaPractice/)、ひらがな版は [Hiragana](https://oviwanazul124.github.io/HiraganaPractice/) です。
