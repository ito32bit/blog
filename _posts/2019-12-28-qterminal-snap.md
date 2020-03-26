---
title: Snap版 Qterminal リリース
date: 2019-12-28
updated: 2020-03-26
categories: Snapリリース
tags: Snap作成
---

Qterminalの Snapパッケージを公開しています。非公式なパッケージです。  
「Qterminal」は LXQtプロジェクトが開発している ターミナルエミュレーターです。
ドロップダウン式ターミナルとしても使用できます。
日本語表示にも対応しています。

開発中の最新版を使用できるように、Snapパッケージを作成しています。

![screenshot]({{ site.baseurl }}/images/qterminal-snap.jpg)

## インストール

Snap Store で公開しています。  
<https://snapcraft.io/qterminal-snap>

GUIの Ubuntuソフトウエア(gnome-software)やスナップストア(snap-store)や KDE Discover からもインストールできます。

![screenshot]({{ site.baseurl }}/images/qterminal-snap_gonome-soft_ja.jpg)

※既にQterminal(debやrpm等)がインストールされていても Snap版をインストール可能です。
設定内容は別々に保存されます。

## 既知の問題

※チェックされている項目は、修正して Edgeチャンネルへ リリース済みです。

- [ ] バージョン番号が「0.14.1」と表示される。実際は開発中の最新の状態です。
- [ ] 更新後(refresh)に起動できなくなる。(バスエラー)  
  回避策： [トラブルシューティング]({{ site.baseurl }}{% post_url 2019-12-28-snap-trouble%})
  ```bash
  sudo snap remove --purge qterminal-snap
  sudo snap install --classic --edge qterminal-snap
  ```
- [x] ドロップダウン式を起動してもドロップダウンできない。
- [X] 端末内から Qtアプリケーションを起動すると問題が起きることがある。  
  原因のひとつは環境変数`QTCHOOSER_NO_GLOBAL_DIR`と思われる。  
  回避策: `export -n QTCHOOSER_NO_GLOBAL_DIR`
- [ ] Fcitx以外で日本語入力できない。

私自身も端末エミュレーターは このSnapパッケージ版 Qterminalを日常的に使用していますので、かなり問題は解消してきたと思います。

## 関連ページ

- [Snapパッケージとは]({{ site.baseurl }}{% post_url 2019-12-28-snap-package %})
