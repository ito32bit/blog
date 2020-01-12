---
title: LXQtをソースからビルドする (Building from source)
date: 2019-08-19
updated: 2019-10-19
categories: ビルド
tags: ビルド LXQtデスクトップ環境 Lubuntu
---
LXQtデスクトップ環境を ソースから ビルドして インストールします。  
LXQt の他に 関連アプリケーションも 一気に ビルドします。  
lxqt-archiver compton-conf obconf-qt lximage-qt qtermwidget  qterminal qps screengrab

LXQtの Wikiを 参考に進めていきます。  
<https://github.com/lxqt/lxqt/wiki/Building-from-source>

## ビルド環境の 準備

ディストリビューション Lubuntu 19.04 i386 [^386]  
カーネル 5.0.0-21-generic  

[^386]: Lubuntu 19.04 の32bit用は、公式ISOがないため cosmicから discoへ 非公式な方法でアップグレードしています。

今回は ビルド作業を デスクトップ環境 Xfce 上で行います。

Lubuntuを起動して LXQtに ログインします。  
端末を起動して、Xfce をインストールします。  
```bash
sudo apt install xfce4 xfce4-goodies
```
<!-- 124MB 使用 -->

再起動して Xfceに ログインします。  
端末 Xfce terminal を起動します。

### Build environment パッケージをインストール
```bash
sudo apt install build-essential cmake git
```
<!-- 28MB -->

### Qt パッケージをインストール
```bash
sudo apt install qtbase5-private-dev libqt5svg5-dev qttools5-dev libqt5x11extras5-dev 
```
<!-- 50MB -->

### KDE components (Frameworks, KScreen) パッケージをインストール
```bash
sudo apt install libkf5guiaddons-dev libkf5idletime-dev libkf5screen-dev libkf5windowsystem-dev libkf5solid-dev
```
<!-- 4MB -->

### その他のパッケージをインストール
```bash
sudo apt install bash libstatgrab-dev libudev-dev libasound2-dev libpulse-dev libsensors4-dev libconfig-dev libmuparser-dev libupower-glib-dev libpolkit-agent-1-dev libpolkit-qt5-1-dev sudo libexif-dev x11-utils libxss-dev libxcursor-dev libxcomposite-dev libxcb-damage0-dev libxcb-dpms0-dev libxcb-screensaver0-dev libxcb-util0-dev libxkbcommon-x11-dev libdbusmenu-qt5-dev libfm-dev libmenu-cache-dev lxmenu-data libgtk2.0-bin hicolor-icon-theme xdg-utils xdg-user-dirs oxygen-icon-theme openbox-dev
```
<!-- 83MB -->

ここまでが LXQtの Wikiを参考に インストールした パッケージです。  
続けて不足している パッケージを インストールします。

### パッケージの 追加インストール
```bash
sudo apt install xserver-xorg-input-libinput-dev xserver-xorg-input-libinput-dev-hwe-18.04 
sudo apt install libxi-dev 
sudo apt install libjson-glib-dev 
```

これで必要なパッケージが インストールできました。

## ソースをダウンロード

```bash
git clone https://github.com/lxqt/lxqt.git
cd lxqt
git submodule init
git submodule update --remote --rebase
```

## ビルド、インストール

次のビルド・コマンドで 一気に ビルドしてインストールします。  
パソコンのスピードによっては、すべて終わるまで とても時間が かかります。
待ちましょう。

```bash
LXQT_PREFIX=/usr ./build_all_cmake_projects.sh
```

エラーなく終了すれば、すべての ビルドとインストール完了です。
もしエラーが発生した場合は、途中で停止します。  

## 新しい LXQtに ログイン

再起動して LXQtに ログインします。  
いろいろ 動かして試してみましょう。

## エラーで 停止した場合には

ビルド中にエラーで停止した場合には、まず表示されたエラーを確認します。  

エラーの例:  
> -- Checking for module 'xi'  
--   No package 'xi' found

この様なエラー表示は インストールされている パッケージ不足の場合があります。  
パッケージ名を調べて インストールします。  
再度 ビルド・コマンドを実行します。

## あとがき

私が、遭遇したエラーのほとんどが パッケージの 追加インストールで解決しました。
しかし、つまずいたエラーもありました。

`Internal error` が出ました。  
この時は、LXQtから ログアウトせずに ビルドしていました。

また同じ `internal error` が出ました。  
原因がわからず・・・数日後・・・  
`sudo apt update` そして `sudo apt upgrade`、
これで最新にしたところ エラーが消えて ビルドできました。  
たった これだけのこと。なんとも これには参りました。

そして、`xi` という パッケージを探す時、  
`apt search xi` とすると沢山でてきて、その多さに ビックリ。
`libxi-dev` を探し当てるのに とても時間がかかりました。  
もっと いい探し方があるのでしょうが、知らないので苦労しました。

苦労しながらも、なんとか ビルドすることが出来ました。  

***
