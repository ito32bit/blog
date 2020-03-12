---
title: Root権限でPCManFM-Qtが起動できない場合
date: 2020-03-10
categories: PCManFM-Qt
tags: PCManFM-Qt トラブルシューティング Debian
---

環境により管理者権限 (Root-instance) で PCManFM-Qtが実行できないことがあります。  
PCManFM-Qtは、LXQtデスクトップ環境のファイルマネージャーですが、LXQt以外の環境でも使用できます。
また Live DVD(USB) 環境で使用することもあります。  
ツールメニューの「rootで開く」（rootとして開く）は、管理者権限で PCManFM-Qtを起動して、GUIでファイル操作ができ大変便利です。  

PCManFM-Qtが rootで開かない時は、次の方法で改善する場合があります。

## PCManFM-Qtの設定を変更する
「編集」メニューの「設定」ダイアログで、「高度」の中の「ユーザー切り替えコマンド」を次のように変更します。

`lxsudo dbus-run-session -- %s`

設定ダイアログのスクリーンショット：[^ver]
![設定ダイアログscreenshot]({{ site.baseurl }}/images/pcmanfm-qt_lxsudo_2020-03.png)

[^ver]: このスクリーンショットは Version 0.14.1の次期リリースの開発版です。`lxsudo` は `lxqt-sudo` コマンド（シンボリックリンクされている）です。

または、次の方法もあります。

## パッケージ dbus-x11 をインストールする
Ubuntuや Debianでは次のように dbus-x11 をインストールします。

```sh
sudo apt install dbus-x11
```

このパッケージをインストールすると、端末内から `sudo pcmanfm-qt` で PCManFM-Qtを起動できるようになります。

## あとがき
この問題は、Debian系だけでなく、Archlinuxや様々なディストリビューションで起きる問題のようです。
もっと知りたい方は、英語で検索してみて下さい。
日本語ではなく英語で検索すると色々と出ててきます。[^e]　
他の解決策があるかもしれません。

[^e]: 私は英語がわからず、英語のサイトは余り理解できていません……

***
