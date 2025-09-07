---
title: "Windows Server 2019 のインストール "
date: 2025-06-09 12:00:10 +0100
categories: [Game Develop]
tags: [Game Develop, Maths, English]
description: 仮想マシンにWindows Server 2019を設定する方法に関する簡単なチュートリアル
math: false
lang: ja
translations:
  ja: /ja/installing-windows-server-2019/
  en: /posts/Installing-windows-server-2019/
  es: /es/installing-windows-server-2019/
permalink: /ja/installing-windows-server-2019/
---

### この投稿は何についてですか？

---

本記事では、Windows Server 2019を仮想マシンにインストールし、他の目的で使用する方法を探求・学習します。このOSの背景を少し説明すると、Windows Serverは、その名が示す通りサーバーでの運用を主眼としたWindowsメインOSの派生版です。市場ではLinuxサーバーディストリビューションがWindows Serverよりも選ばれる傾向にありますが、企業向けアプリケーションとの互換性（Linuxでは現在または将来的に動作しない可能性があるもの）を理由に、依然としてWindows Serverを選択する企業も存在します。こうした背景から、Windows Server 2019が一般的に使用されるケースが多いです。システムが長期間更新されていない場合や、他の新バージョンよりもこのOSに関する情報や経験が豊富であることが理由です。背景が少し理解できたところで、本題に入ります。

---

### 従うべき手順

#### OS用仮想化システムのインストール

まず最初に行うべきことは、OS用の仮想化システム（一般に仮想マシンとして知られています）をインストールすることです。このチュートリアルでは、Oracle社の[VirtualBox](https://www.virtualbox.org/)を使用します。インストールするには[こちら](https://www.virtualbox.org/wiki/Downloads)をクリックしてください。 

> VirtualBox Extension Packもインストールすることをお勧めします。これにより機能が追加されます。詳細を知りたい場合は[こちら](https://docs.oracle.com/en/virtualization/virtualbox/6.0/user/intro-installing.html)をクリックしてください。
{: .prompt-info }

![VirtualBox-Main-Download-Page](assets/photos/Installing-Windows-Server-2019/Virtual-Box-Main-Page.png)
_VirtualBox メインダウンロードページ_

#### Windows Server 2019 ISOの入手

次に、Windows Server 2019のISOをインストールする必要があります。そのためには、こちらの[ウェブサイト](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)にアクセスし、必要な言語とバージョンを選択してください。

> ダウンロードされるのはWindows Server 2019 ISO試用版であることをご留意ください。このバージョンは約120日後にすべてのファイルを消去します。実際のシステム展開にご利用の場合は、ライセンスを取得するか、重要なファイルをこのシステムに保存しないでください。
{: .prompt-warning}

![WindowsServer-Main-Download-Page](assets/photos/Installing-Windows-Server-2019/Windows-Server-2019-Main-Down-Page.png)
_Windows Server メインダウンロードページ_


#### VirtualBoxの設定

##### ISOの情報

VirtualBoxとWindows Server 2019のISOをインストールしたところで、「新規」ボタンを押します。すると新しいページが開き、仮想マシンの名前、保存場所、エミュレートするOSの選択を求められます。ISOイメージを選択するだけでこれらの質問にすべて答えるため、手動で入力する必要はありません。

Windows ADK を使用したテストを行わない場合、または無人インストールを実行しない場合は、すべてのチェックマークを無効にできます。

> Windowsの無人インストールとは、Windows ADKを使用して事前設定済みの構成でインストールを開発する手法であり、複数のデバイスにインストールを行う場合に実施する価値がある。
{: .prompt-info}

![VirtualBox-Main-Configuration-page](assets/photos/Installing-Windows-Server-2019/Configure-Page-VirtualBox.png)
_VirtualBox メイン設定ページ_

##### ハードウェア構成

次に、マシンに使用させたいメモリとプロセッサを割り当てる必要があります。これはお使いのシステムによって異なるため、テストすることをお勧めします。Windows Server 2019 の最小要件は以下の通りです：

- サーバー環境: 2GB / GUI環境: 4GB (詳細は後述のセクションで説明します)

- コア数は実行するアプリケーションに依存しますが、OSのみの場合は2コアで動作可能。推奨は少なくとも4コア

![VirtualBox-Hardware-Page](assets/photos/Installing-Windows-Server-2019/Virtual-Box-Hardware-Page.png)
_VirtualBox ハードウェア設定ページ_

##### 仮想ディスク構成

次に仮想マシンに空き領域を確保します。ハードウェアセクションと同様、お使いのデバイスによって異なりますが、最低限必要なのは以下の通りです：

- 32GBの空き領域

![VirtualBox-Virtual-Disk-Page](assets/photos/Installing-Windows-Server-2019/Virtual-Box-Disk-Configuration-Page.png)
_VirtualBox 仮想ディスク ページ_

#### OSの設定

すべて正しく行われた場合、この画面に到達します。ここで言語、タイムゾーン、キーボード設定を選択します。

> 私が提供したリンクからダウンロードした場合、それ以上の選択肢はありません。なぜならISOイメージは1言語のみ対応しているからです。
{: .prompt-info}

![WindowsServer-Startup-Page](assets/photos/Installing-Windows-Server-2019/Windows-Server-2019-Startup-Page.png)
_Windows Server インストール スタートアップ ページ_

次のオプションは次のとおりです：

- Windows Server 2019 Standard Edition (GUI付き/なし)

- Windows Server 2019 Datacenter Edition (GUI付き/なし)

使用するべきバージョンを知りたい場合は、Microsoftのこの[ガイド](https://learn.microsoft.com/en-us/windows-server/get-started/editions-comparison?pivots=windows-server-2019)を参照し、両方のバージョンがどのようなものか確認してください。

![WindowsServer-Edition-Selection-Page](assets/photos/Installing-Windows-Server-2019/Windows-Server-2019-Selection-Edition-Screen.png)
_Windows Server 2019 エディション選択ページ_

最後にやるべきことは、システムがデフォルトで設定しているパスワードを変更することです 

![WindowsServer-Pass-Page](assets/photos/Installing-Windows-Server-2019/Windows-Server-2019-Change-Pass-Pg.png)
_Windows Server 2019 パスワード変更_

#### 終幕

これで仮想マシンへのWindows Server 2019のインストールは完了しました。今後、このテーマを中心としたチュートリアルをさらに公開していきます。
