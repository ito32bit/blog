---
title: LXQtを最新の日本語表示にする
date: 2020-01-13
updated: 2020-11-05
categories: LXQtデスクトップ環境
tags: LXQtデスクトップ環境 LXQt翻訳
---
LXQtデスクトップ環境に 最新の日本語訳を 適用する方法です。  
４つ方法を紹介します。  

## Snap版 LXQt 言語パック をインストールする

<https://snapcraft.io/lxqt-l10n-snap>  

LXQt言語パックの Snapパッケージ版を作成 [^ln] しました。
Ubuntu等、snapd がインストールされている環境であれば、次の方法でこのLXQt言語パックをインストールできます。  
一度インストールすれば、定期的に自動更新されて最新の翻訳ファイルが適用されます。  

端末の場合、次の２つのコマンドを実行後に再ログインします。  

[^ln]: lxqt-l10n-snap (Snap版LXQt言語パック)は、2020年１月現在、最新の日本語が表示されない問題があります。(デスクトップマネージャー、ファイルマネージャー等)

```bash
sudo snap install lxqt-l10n-snap --edge 
/snap/lxqt-l10n-snap/current/setup
```

Lubuntu 等は Snapパッケージのインストール前に snapd のインストールが必要です。  
Snap版 LXQt言語パックの詳細: [Snap版 LXQt言語パック リリース]({{ site.baseurl }}{% post_url 2020-01-13-lxqt-l10n-snap %})

この方法が 下記の方法に比べて、 簡単に 日本語表示を新しく出来ると思います。  

## Weblateから翻訳ファイルをダウンロードする  

<https://translate.lxqt-project.org/languages/ja/>  
  
- ここから各翻訳ファイル(拡張子.ts)をダウンロードします。  
- .tsファイルを .qmファイルに変換します。(lreleaseコマンド)  
- 各ディレクトリの 既にある .qmファイルに上書きします。
- ログアウト＆再ログインします。  

ディレクトリは Ubuntu18.04の場合： /usr/share/lxqt/translations/  

どのディストーションでも手軽に出来ると思いますが、とても手間がかかります。
ひとつ ひとつでも 日本語に出来ますが、すべてとなると 40以上あります。  
この方法では アプリケーションメニューの中の 名称(デスクトップエントリ)は 変更できません。

## Githubから 開発中のLXQtをダウンロードしてビルドする  

<https://github.com/lxqt/lxqt/wiki/Building-from-source>  

LXQtの Wikiに方法が書かれています。  
git clone して ビルドします。  

ビルド環境が必要です。Wikiに詳しく書いてあります。（英語です）  
ビルドの実例: [LXQtをソースからビルドする]({{ site.baseurl }}{% post_url 2019-08-19-building-lxqt-source %})  

※Weblateに登録された翻訳が、Githubに取り込まれる(マージ)までに タイムラグがあります。
間隔は不定期で、数日から １周間程度遅れていると思います。

## 日本語翻訳ファイルセット(zipファイル)をダウンロードする  

<https://github.com/ito32bit/lxqt-ja>  

これは LXQt 0.14.ｘ 用です。
(0.15.0以降では適用されています。)

緑色のボタン「Clone or download」をクリック。zipファイルを ダウンロードします。  
使用方法は リンク先の下部に あります。  

日本語の表示確認に使用している 日本語翻訳ファイルを セットにして ダウンロード出来るようにしました。  
Ubuntu 18.04 LXQt 0.14.1 で表示確認しています。
他の ディストリビューションでも 使用できると思います。

***
