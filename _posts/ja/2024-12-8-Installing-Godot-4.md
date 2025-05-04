---
title: Godot 4のインストール 
date: 2024-12-8 12:00:10 +0100
categories: [Game Develop]
tags: [Godot, Game Develop, Tutorial, English]
description: これはGodotをダウンロードするためのかなり簡単なチュートリアルです。
lang: ja
image:
  path: assets/photos/Develop-an-RPG/GodotMainPage.png
  alt: Godot Enginge Web Page
permalink: /ja/installing-godot-4/
translations:
  ja: /ja/installing-godot-4/
  en: /posts/Installing-Godot-4/
  es: /es/installing-godot-4/
---

## 序論

この連載では、GodotでRPGゲームを開発する方法を見ていきます。ビデオゲームを開発する際に使用できるエンジンは、**Unity**や**Unreal Engine**など数多くありますが、ここでは以下の理由から**Godot**を選択します。

## なぜ Godot なのか？

Godotはオープンソースの**無料で使える**エンジンです。その開発のために寄付することもできますが、もしあなたがこの趣味を始めようとしているのなら、このエンジンは**最高のエンジン**の一つだと私は思います。

すべてが完璧というわけではなく、**欠点**もあります。たとえば、コミュニティがやや小さいので、**特定のチュートリアルを見つけるのが**難しく**、**ドキュメンテーション**を参照する必要があります。また、Godotは独自のGDScript**言語を使用しますが、これはPythonやRubyなどの他の言語と似ています。

## エンジンの取り付け

### ホームページより

エンジンをインストールするには、2つの方法がある。1つ目は、公式ウェブサイトからダウンロードする方法だ！

![Godot-Main-Page](assets/photos/Develop-an-RPG/GodotMainPage.png)
_Godot ホームページ_

### デジタルショップから

2つ目の方法は、Steamやitch.io、Epic Games Storeなどのデジタルショップを利用する方法だ。

![Godot-Steam-Page](assets/photos/Develop-an-RPG/GodotSteamPage.png)
_スチームGodotホームページ_

> オンラインショップからインストールすると、C#のサポートが無効になるので、使用したい場合は公式サイトからダウンロードすること。
{: .prompt-warning }

## 新規プロジェクトの作成

開くとこのように表示されるので、次にすることは赤でマークされたボタンのクリックだ。

![Godot-Projects-Open](assets/photos/Develop-an-RPG/GodotProjectsOpen.png)
_Godot プロジェクト・エクスプローラー_

ボタンを押すとこのように表示されます。

![Godot-Projects-Create](assets/photos/Develop-an-RPG/GodotProjectsCreate.png)
_Godot でプロジェクト・ウィンドウを作成する_

ここでは、**プロジェクトの名前**と**保存場所**を設定する必要があります。また、プロジェクトのレンダリング方法を選択することもできますが、ここでは **Forward+** を選択し、**Create and Edit** をクリックします。

![Godot-Engine-Open](assets/photos/Develop-an-RPG/GodotEngineOpen.png)
_オープンエンジン_

これでGodotのインストールは完了です。次のチュートリアルでは、スプライトを追加する方法と、動きのタイプを選択する方法を見ていきましょう。
