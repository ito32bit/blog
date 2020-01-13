---
title: LXQtを最新の日本語表示にする
date: 2020-01-13
updated: 2020-01-13
categories: LXQtデスクトップ環境
tags: LXQtデスクトップ環境 日本語 翻訳
---
LXQtデスクトップ環境に 最新の日本語訳を 取り入れる方法です。  
４つ方法を紹介します。  

## Snap版 LXQt 言語パック をインストールする

<https://snapcraft.io/lxqt-l10n-snap>  

Snapパッケージを作成しました。
Ubuntu等、snapd がインストールされている環境であれば、次の方法でこの言語パックをインストールできます。  
端末の場合、次の２つのコマンドを実行後に再ログインします。  

```bash
    sudo snap install lxqt-l10n-snap --edge 
    /snap/lxqt-l10n-snap/current/setup
```

こちらの方法が 下記の方法に比べて、 簡単に 日本語表示を新しく 出来ると思います。  
Lubuntu 等は snapd のインストールが必要です。`sudo apt install snapd`  
snapd のインストール: <https://snapcraft.io/docs/installing-snapd>  

※2020年１月現在、この言語パックは作成中のため 最新の日本語が表示されない問題があります。
(デスクトップマネージャー、ファイルマネージャー等)

## Githubから 開発中のLXQtをダウンロードしてビルドする  

<https://github.com/lxqt/lxqt/wiki/Building-from-source>  

LXQtの Wikiに方法が書かれています。  
git clone して ビルドします。  

ビルド環境が必要です。詳しく書いてあります。ArchLinuxだと 簡単のようです。  
ビルドの実例: [[LXQtをソースからビルドする]]  

※Weblateに登録された翻訳が、Githubに取り込まれる(マージ)までに タイムラグがあります。
間隔は不定期で、数日から １ヶ月程度遅れていると思います。

## Weblateから翻訳ファイルをダウンロードする  

<https://weblate.lxqt.org/languages/ja/lxqt/>  
  
- ここから各翻訳ファイル(拡張子.ts)をダウンロードします。  
- .tsファイルを .qmファイルに変換します。(lreleaseコマンド)  
- 各ディレクトリの 既にある .qmファイルに上書きします。
- ログアウト＆再ログインします。  

ディレクトリは Ubutu18.04の場合： /usr/share/lxqt/translations/  

どのディストーションでも手軽に出来ると思いますが、とても手間がかかります。
ひとつ ひとつでも 日本語に出来ますが、すべてとなると 40以上あります。  
この方法では アプリケーションメニューの中の 名称(デスクトップエントリ)は 変更できません。

## 日本語翻訳ファイルセット(zipファイル)をダウンロードする  

<https://github.com/ito32bit/lxqt-ja>  

緑色のボタン「Clone or download」をクリック。zipファイルを ダウンロードします。  
使用方法は リンク先の下部に あります。  

日本語の表示確認に使用している 日本語翻訳ファイルを セットにして ダウンロード出来るようにしました。  
Ubuntu 18.04 LXQt 0.14 で表示確認しています。
他の ディストリビューションでも 使用できると思います。
