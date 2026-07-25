---
title: Godot 4のインストール

date: 2024-12-8 12:00:10 +0100

categories: [Game Develop]

tags: [Godot, Game Develop, Tutorial, Japanese]

excerpt: これはGodotをダウンロードするためのかなり簡単なチュートリアルです。

toc: true
toc_sticky: true

header:
  teaser: /assets/images/Develop-an-RPG/GodotMainPage.png
  overlay_image: /assets/images/Develop-an-RPG/GodotMainPage.png
  overlay_filter: 0.25

language: jp
ref: installing-godot-4
lang_en: /en/installing-godot-4
lang_es: /es/installing-godot-4
lang_ja: /jp/installing-godot-4
permalink: /jp/installing-godot-4
---

現在も日本語を勉強中ですので、この投稿では翻訳ツールを利用しました。もし誤りを見つけた場合は、修正のためご連絡ください。よろしくお願いします。
{: .notice--danger }

## 序論

この連載では、GodotでRPGゲームを開発する方法を見ていきます。ビデオゲームを開発する際に使用できるエンジンは、**Unity**や**Unreal Engine**など数多くありますが、ここでは以下の理由から**Godot**を選択します。

## なぜ Godot なのか？

Godotはオープンソースの**無料で使える**エンジンです。その開発のために寄付することもできますが、もしあなたがこの趣味を始めようとしているのなら、このエンジンは**最高のエンジン**の一つだと私は思います。

すべてが完璧というわけではなく、**欠点**もあります。たとえば、コミュニティがやや小さいので、**特定のチュートリアルを見つけるのが**難しく**、**ドキュメンテーション**を参照する必要があります。また、Godotは独自のGDScript**言語を使用しますが、これはPythonやRubyなどの他の言語と似ています。

## エンジンの取り付け

### ホームページより

エンジンをインストールするには、2つの方法がある。1つ目は、公式ウェブサイトからダウンロードする方法だ！

![Godot-Main-Page](/assets/images/Develop-an-RPG/GodotMainPage.png)

### デジタルショップから

2つ目の方法は、Steamやitch.io、Epic Games Storeなどのデジタルショップを利用する方法だ。

![Godot-Steam-Page](/assets/images/Develop-an-RPG/GodotSteamPage.png)

オンラインショップからインストールすると、C#のサポートが無効になるので、使用したい場合は公式サイトからダウンロードすること。
{: .notice--warning }

## 新規プロジェクトの作成

開くとこのように表示されるので、次にすることは赤でマークされたボタンのクリックだ。

![Godot-Projects-Open](/assets/images/Develop-an-RPG/GodotProjectsOpen.png)

ボタンを押すとこのように表示されます。

![Godot-Projects-Create](/assets/images/Develop-an-RPG/GodotProjectsCreate.png)

*Godot でプロジェクト・ウィンドウを作成する*ここでは、**プロジェクトの名前**と**保存場所**を設定する必要があります。また、プロジェクトのレンダリング方法を選択することもできますが、ここでは **Forward+** を選択し、**Create and Edit** をクリックします。

![Godot-Engine-Open](assets/images/Develop-an-RPG/GodotEngineOpen.png)

これでGodotのインストールは完了です。次のチュートリアルでは、スプライトを追加する方法と、動きのタイプを選択する方法を見ていきましょう。
