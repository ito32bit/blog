---
title: Snap版 LXQt言語パック　内部の仕組み
date: 2020-01-15
categories: ビルド
tags: Snap作成 LXQt翻訳 LXQtデスクトップ環境
---
私が作成している「[Snap版 LXQt言語パック リリース]({{ site.baseurl }}{% post_url 2020-01-13-lxqt-l10n-snap %})」(lxqt-l10n-snap) の技術情報です。 [^g]  
内部の仕組みについて紹介します。

[^g]: 当初、ひとつのページでしたが、読みやすくするため技術情報のページを分けました。

## インストールについて

このSnapは、`/snap/lxqt-l10n-snap/` ディレクトリにインストールされます。
この中に `*.qm` や `*.desktop` や `*.directory` ファイルが配置されます。  

Snapパッケージをインストール後に、ログインしている各ユーザーで次のコマンドを実行します。  
　　`/snap/lxqt-l10n-snap/current/setup`  
すると `$HOME/.config/lxqt/session.conf` 内の環境変数が設定されます。
設定内容は、LXQt設定 → セッション → 環境 で確認できます。
このコマンドを使わずに（.xsessionrc 等に）次のように自分で設定することも出来ます。

```bash
export XDG_CONFIG_DIRS=/snap/lxqt-l10n-snap/current/etc/xdg:$XDG_CONFIG_DIRS
export XDG_DATA_DIRS=/snap/lxqt-l10n-snap/current/usr/share:$XDG_DATA_DIRS
```

## 環境変数について

LXQtデスクトップ環境は、ツールキットQt5を使用して開発されていて、各アプリケーションは環境変数を参照しているようです。

環境変数 `XDG_DATA_DIRS` に Snapのディレクトリを追加して、翻訳ファイル `*.qm` を参照するようにしています。
アプリケーションメニューも この環境変数を参照しています。
しかし `*.directory` も配置してありますが、参照されないようです。  
それから PCManFM-Qtは、この環境変数を見ていないかも知れません。

LXQt設定の セッションの LXQtモジュール名については、環境変数 `XDG_CONFIG_DIRS` に Snapのディレクトリを追加して `*.desktop` を参照するようにしています。

LXQt設定 → セッションのスクリーンショット　環境変数に設定を確認できる:  
![session screenshot]({{ site.baseurl }}/images/lxqt-config-session_ja_screen-2020-01.jpg)

## 動作確認している環境

Ubuntu 18.04 LXQt 0.14 (Github からインストール)  
Lubuntu 18.04 LXQt 0.14 (ppa)  

## ビルド

どのように Snapパッケージをビルドしているか紹介します。

ビルド状況は 次のページで見られます: 
[![Snap Status](https://build.snapcraft.io/badge/ito32bit/lxqt-l10n-snap-packaging.svg)](https://build.snapcraft.io/user/ito32bit/lxqt-l10n-snap-packaging)

ソース snapcraft.yaml ファイルは次のリンク先で公開しています。  
Github : <https://github.com/ito32bit/lxqt-l10n-snap-packaging>

Githubの関連リポジトリが更新(commit)があると、build.snapcraft.ioサイト内で 自動でビルドされます。
関連リポジトリのリストは、snapcraft.yaml ファイルの partsの `source:` です。  

LXQtの各リポジトリを Git clone して、bashスクリプトで翻訳ファイルとデスクトップエントリのファイルを処理しています。  
ソースからビルドする際に使用する cmake や make コマンドは使用していません。 [^cm]

[^cm]: 自分で 言語パック用 CMakeLists.txt を用意すると良いのでしょうけれども、私には CMakeLists.txt の書式などが分からず作れません。それで独自の bashスクリプトを書きました。

提案や質問などがありましたら、気楽にコメントやプルリクエストして下さい。

## 関連ページ

- [Snap版 LXQt言語パック　リリース]({{ site.baseurl }}{% post_url 2020-01-13-lxqt-l10n-snap %})
- [Snapパッケージとは]({{ site.baseurl }}{% post_url 2019-12-28-snap-package %})
- [LXQtを最新の日本語表示にする]({{ site.baseurl }}{% post_url 2020-01-13-lxqt-japanese %})

***
