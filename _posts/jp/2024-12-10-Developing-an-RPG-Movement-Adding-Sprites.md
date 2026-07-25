---
title: GodotでのRPG開発 - 移動とスプライトの追加

date: 2024-12-14 12:00:10 +0100

categories: [Game Develop]

tags:
  - Godot
  - Game Develop
  - Tutorial
  - Maths
  - Japanese

excerpt: これはGodotでRPGゲームを開発する方法についてのブログ記事シリーズです。今回の記事では、移動とスプライトの追加について取り上げます。

toc: true
toc_sticky: true
use_math: true

header:
  overlay_image: /assets/images/Develop-an-RPG-2/Header.gif
  overlay_filter: 0.25

language: jp
ref: developing-RPG-adding-sprites
lang_en: /en/developing-RPG-adding-sprites
lang_es: /es/developing-RPG-adding-sprites
lang_ja: /jp/developing-RPG-adding-sprites
permalink: /jp/developing-RPG-adding-sprites
---

## 運動

現在も日本語を勉強中ですので、この投稿では翻訳ツールを利用しました。もし誤りを見つけた場合は、修正のためご連絡ください。よろしくお願いします。
{: .notice--danger }

ビデオゲームにおいて最も基本的な要素の一つは動きであり、動きの要素を全く含まないゲームは稀ですが、存在はします。しかし、ここでは2Dゲームにおける動きに焦点を当ててみましょう。

### 2次元運動の数学と物理学

まず、2Dでの動きの仕組みを理解し、その上で3次元について議論する必要があります。3Dの動きについては、今後のブログ記事で取り上げます。簡単に言えば、ビデオゲームにおける動きはベクトルから生まれます。

$$\vec{B}=\begin{bmatrix}\vec{i} \vec{j}\end{bmatrix}$$

![Vector-Base](/assets/images/Develop-an-RPG-2/Vector-Base.png)

**i** は **x** や **j** と同じであり、**y** と同じである。.
{: .notice--info}

運動は、ベクトルが変化したときに生じる。例えば、運動のためのベクトル**u**を定義すると.

$$\vec{u}=\begin{bmatrix}  0, 0\end{bmatrix}$$

このベクトルは、キャラクターが x = 0、y = 0 の位置にあることを示しています。しかし、例えばキャラクターを2回上に移動させると、このベクトルは変化します。

$$\vec{u}=\begin{bmatrix}  0, 2 \end{bmatrix}$$

![Vector-Example](/assets/images/Develop-an-RPG-2/Vector-Example.png)

ベクトル u はベクトル j の2倍で構成されていることに注目してください。

$$\vec{u}=\begin{bmatrix}  2\vec{i}, 0\end{bmatrix}$$

これは、ビデオゲームにおける非常に基本的な動きを理解するための最も基本的な要素です。今後、さらに発展させていきます。

## Godotでの動き

### 簡単な説明

クラシックRPGでは8方向移動を採用しており、この移動方式によりプレイヤーは**W**、**A**、**S**、**D**キーを使用して8方向に移動できます。

まず最初に、プロジェクトのルートディレクトリに「Scripts」という名前の新しいフォルダを作成する必要があります。ここに、ゲームで使用するすべてのスクリプトを保存します。

![Godot-Explorer-Created-Scripts](/assets/images/Develop-an-RPG-2/Created-Folder-Scripts.png)

「Scripts」フォルダを作成した後、左クリックして新しいスクリプトを作成します。

### コード

これから書くコードは次のとおりです：

```gdscript
extends CharacterBody2D
```

では、このコード行 **extends CharacterBody2D** を理解しましょう。「extends」は、[CharacterBody2D](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html)に関連するすべての関数をインポートする役割を担っています。

CharacterBody2Dについてもっと知りたい場合は、その名前をクリックすると、Godotの公式ドキュメントにリダイレクトされます。
{: .notice--info}

#### 変数

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800
```

次に、2行の新しいコードを追加します。覚えていない方のために、変数は **var [変数名] = [値]** で定義されます。では、横にある @export は何を意味するのでしょうか？「@」の横にある単語は、その変数に対して何かを行う必要があることを示すために使用されます。この場合は、エディタにエクスポートすることを意味します。つまり、エディタに戻ると、その変数がエディタに表示されるということです。

#### 機能

次に、このスクリプトの2つの主要な関数を定義します。1つ目は**get_input()**で、その名前が示す通り、プレイヤーの入力を取得する関数です。もう1つの関数は**\_physics_process(delta)**で、これはGodotのいくつかのノードに付属する関数であり、各フレーム内でコードを呼び出す役割を担います。

デルタ変数はビデオゲーム開発において非常に重要な変数であり、今後ブログでさらに詳しく解説していきます。
{: .notice--info}

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800

func get_input():
  pass

func _physics_process(delta):
  pass
```

### 機能 get_input()

それでは、**get_input()**関数に注目しましょう。この関数は、入力キーである**左**、**右**、**上**、**下**から得られる方向ベクトルを取得する役割を担っています。では、これらの入力キーとは何でしょうか？それについては後ほど説明します。まずは、ここにあるif文について話しましょう。このif文は、プレイヤーが走りたいのか歩きたいのかを確認する役割を担っています。**shift**キーが押されている場合、コードは変数**running_speed**を使用しますが、押されていない場合は**walking_speed**を使用します。

```gdscript
func get_input():
  var input_direction = Input.get_vector("left", "right", "up", "down")
  if Input.is_action_just_pressed("shift"):
    velocity = input_direction * running_speed
  else:
    velocity = input_direction * walking_speed
```

#### 入力コマンドの設定

入力マップを開くには、以下の手順に従います。まず、**プロジェクト**に移動し、次に**プロジェクト設定**を選択し、最後に**入力マップ**を選択します。

![Godot_Input_Map](/assets/images/Develop-an-RPG-2/Godot-Input-Map-Window.png)

その後、**「新しいアクションを追加」**と表示されている箇所に、**left**と入力し、**追加**をクリックします。クリックすると、以下の変更が表示されます。

![Godot_Input_Map_Added_Input](/assets/images/Develop-an-RPG-2/Godot-Iput-Map-Added-Input.png)

次に、**プラス記号**をクリックし、その入力欄に追加したいキーを押します。その後、**OK**をクリックします。

![Godot_Input_Map_Added_Input_Key](/assets/images/Develop-an-RPG-2/Godot-Input-Map-Added-Input-Key.png)

次に、**右**、**上**、**下**キーについても同じ手順を実行する必要があります。

#### Función \_physics_process(delta)

次に、**\_physics_process(delta)** 関数について説明します。この関数はエンジン自体によって作成され、物理演算に関連する処理を担当します。ここから、前述の関数 **get_input()** と、エンジンによって作成された関数 **move_and_slide** を呼び出します。この関数は、オブジェクトがいつ移動すべきかを指示します。

```gdscript
  func _physics_process(delta):
    get_input()
    move_and_slide()
```

**delta**で通知を受け取った場合は、次のようにハイフンを追加してください：「**\_delta**」
{: .notice--warning}

## Añadiendo el script y creando el jugador

次に、**Node2D**を左クリックし、**子を追加**を押します。するとウィンドウが開くので、**CharacterBody2D**を探して追加します。

![Adding_CharacterBody2D](/assets/images/Develop-an-RPG-2/Adding-CharacterBody2D.gif.gif)

もしそこに**Node2D**がない場合は、characterBody2Dを追加したのと同じ方法で追加してください。
{: .notice--warning}

その名前の横に小さな警告アイコンが表示されますが、今のところ気にしないでください。その後、同じ操作を再度行い、今度は**CharacterBody2D**をクリックして、**Sprite**を追加してください。

![Adding_Sprite](/assets/images/Develop-an-RPG-2/Adding-Sprite.gif)

あとは、CharacterBody2Dにスクリプトを追加するだけです。

![Adding_Script_To_CharacterBody2D](/assets/images/Develop-an-RPG-2/Adding-Script-To-CharaterBody2D.gif)

## Github デモ

こちらからアクセスできます [repo](https://github.com/oviwanazul124/How-to-make-an-RPG/tree/main/Developing%20an%20RPG%20in%20Godot%20-%20Movement%20and%20adding%20sprites) RPGの開発過程における様々なファイルが含まれています。
