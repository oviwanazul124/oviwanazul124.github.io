---
title: C言語によるライプニッツのアルゴリズム

date: 2024-12-7 17:42:10 +0100

categories: [Coding]

tags:
  - C
  - Tutorial
  - Japanese

excerpt: ライプニッツのアルゴリズムをC言語で開発する方法についての短い講義

toc: true
toc_sticky: true

use_math: true

language: jp
permalink: /jp/leibniz-algorithm
ref: leibniz-algorithm
lang_en: /en/leibniz-algorithm
lang_es: /es/leibniz-algorithm
lang_ja: /jp/leibniz-algorithm
---

現在も日本語を勉強中ですので、この投稿では翻訳ツールを利用しました。もし誤りを見つけた場合は、修正のためご連絡ください。よろしくお願いします。
{: .notice--danger }

## 簡単な紹介

ライプニッツのアルゴリズムをC言語で開発するには、まずそのアルゴリズムが何に基づいているかを知らなければならない。以下はそのアルゴリズム/系列の数式である。

$$\sum_{n=0}^\infty\frac{(-1)^n}{2n + 1} = \frac{\pi}{4}$$

## プロセスの説明

### 図書館を含む

まず、以下のライブラリをインポートする必要がある。

```c
#include <stdio.h>
#include <math.h>
```

必ず輸入しなければ、将来的に問題が発生する。
{: .notice--danger }

「stdio」ライブラリーはCの標準的なライブラリーであり、「math.h」はより高度な数学を扱うために使用するライブラリーである（上記で説明した別の方法を使用する場合は、このライブラリーをインポートする必要はない）。

### すべての変数を含む

次にしなければならないのは、実行されるさまざまな反復を表示するための変数**イター**と、ユーザーが最初に入力した各反復をカウントするための変数**カウンタ**の設定である。

```c
int iter;
int count = 0;
float pi = 3.141592653589793;
```

### 機能

最初の関数は「**introduction()**」と呼ばれる関数で、ユーザーを歓迎し、数字を紹介する役割を果たします。

```c
// グローバル機能

void introduction();
void serie();
```

## 導入機能

この関数は、円周率を計算する反復回数を要求する。 [すべての変数を含む](#すべての変数を含む).この後、それが0か負であるかをチェックする。もしそうであれば、エラーとなるため、再度ユーザーに反復回数を尋ね、最後に [セリエ機能](#セリエ機能).

```c

printf("繰り返しの回数を入力してください。 \n");
scanf("%i", &iter);

    while(iter <= 0){
        printf("0以下の数字を入力したようですが、正の数を入力してください。 \n");
        scanf("%i", &iter);
    }
    serie();
```

念のために言っておく、 ‘\n’ を使うと、ターミナルの次の行に次のようなメッセージが表示される。
{: .notice--info }

## セリエ機能

次に、変数**cont**が提案された反復回数より大きくなるまで実行するwhileを使用します。次に行うことは、変数**d**を作成することで、これは冒頭で示した[数式](#簡単な紹介)の分数を担当します。次に、**result**という別の変数を定義し、これは分数によって得られた結果を加算することを担当します(そうしないとπではなくπ/4が得られるため、4倍します)。

```c
 printf("iter, error, result \n");
    while(cont < iter){
        double d;
        d = ((powf(-1, cont)) / (2*cont + 1));
        double result;
        result += (d*4);
        cont += 1;
        double error = fabs(((pi - result) / pi) * 100);
        printf("%4i, err:%4e, %4lf \n", cont, error, result);
    }
  cont = 0;
  introduccion();
```

ご存じないかもしれませんが, なぜなら、C言語では1つの変数に格納できるバイト数に制限があるからである。
{: .notice--info }

## Final Code

最終的なコードは私の[github](https://github.com/oviwanazul124/Leibniz-s-Algorithm-in-C/blob/main/main.c)ページにある。
