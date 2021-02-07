---
title: LXQtデスクトップ環境の翻訳
date: 2019-12-28
updated: 2021-01-31
categories: 翻訳
tags: LXQt翻訳 LXQtデスクトップ環境 Lubuntu Debian
---

私は、LXQtデスクトップ環境の翻訳をしています。  
次の技術評論社の記事を読んだのを きっかけに翻訳を始めました。

第552回　デスクトップ環境の2018-2019年  
<https://gihyo.jp/admin/serial/01/ubuntu-recipe/0552?page=2>

現在、LXQt自体については英語表記がなくなりました。
既に翻訳されている部分についても、より良くするために少しずつ変更しています。  
多くの人が、パッと見て 考えたり悩んだりせずに 軽快に 操作できるような日本語の表示にしたいと思っています。

LXQtを使用していて、日本語で気になる部分もあるかと思います。その時は、遠慮なくコメント（提案）して下さい。
[Weblate](https://translate.lxqt-project.org/)でも Github [Discussions](https://github.com/ito32bit/lxqt-ja/discussions) でも、どちらへのコメントでも構いません。

Weblate は参加（登録）するのも簡単です。
翻訳の「提案」は登録無しで出来ます。

**2020年１月**  
技術評論社サイトの いくやさんの記事に載りました。  
「第601回　デスクトップ環境の2019-2020年」 <https://gihyo.jp/admin/serial/01/ubuntu-recipe/0601?page=2>  
いくやさんのブログにも <https://blog.goo.ne.jp/ikunya/e/f812563dd2e30fa48f73b3845f133157>  

LXQtデスクトップ環境のスクリーンショット:  
![LXQt screenshot]({{ site.baseurl }}/images/lxqt-2020-01.png)

## 翻訳に参加しているソフトウェア

### LXQtプロジェクト
- LXQt - デスクトップ環境
- PCManFM-Qt - ファイルマネージャー
- LXImage-Qt - 画像ビューアー
- Qterminal - 端末
- Qps [^qps] - プロセスマネージャー
- LXQt-Archiver - アーカイバー (圧縮・展開)
- ScreenGrab - スクリーンショット
- Obconf-Qt - Openboxの設定ユーティリティ
- ComptonConf - Comptonの設定ユーティリティ
- pavucontrol-qt - PulseAudio音量調節

<https://github.com/ito32bit/lxqt-ja/wiki>  

[^qps]: Qpsにはシステムに関する専門用語が多く、知識不足のため未翻訳の部分があります。

### LXQt関連の翻訳
- FeatherNotes - 階層型のメモ管理 (HTML出力機能付き)  [^n]
- FeatherPad - テキストエディター
- Kvantum - Qtテーマ Kvantum スタイルエンジン (表示・編集)  [^k]

[^n]: FeatherNotesには まだ未翻訳が多くあります。是非あなたも翻訳に参加して下さい。１個の部分（文字列）からでも始められます。まずは **提案** をしてみましょう。

[^k]: Kvantumには専門用語が多く、知識不足のため未翻訳の部分があります。わかる方 いらっしゃいませんか？

### Lubuntu(18.10以降)関連の翻訳
- nm-tray - NetworkManagerフロントエンド (タスクトレイ)
- Qlipper - クリップボード履歴 (タスクトレイ)

### Debian関連の翻訳
- lxqt(29) - パッケージ説明文  <https://packages.debian.org/bullseye/lxqt>
- task-lxqt-desktop(3.58) - パッケージ説明文 <https://packages.debian.org/bullseye/task-lxqt-desktop>
- Meteo-qt - lxqtメタパッケージに含まれている 天気予報（気象情報）アプリ[^me]

[^me]: Meteo-qtは気象の専門用語に詳しくないため未翻訳の部分や直訳のため変な日本語があります。また、アプリのバグか私の理解不足か、風力の表示に変な部分があります。

## 関連ページ

- [LXQtを最新の日本語表示にする]({{ site.baseurl }}{% post_url 2020-01-13-lxqt-japanese %})
- [Snap版 LXQt言語パック リリース]({{ site.baseurl }}{% post_url 2020-01-13-lxqt-l10n-snap %})
- LXQt 翻訳サイト <https://translate.lxqt-project.org/>

***
