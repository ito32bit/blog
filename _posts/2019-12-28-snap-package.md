---
title: Snapパッケージとは
date: 2019-12-28 00:00:00
updated: 2020-01-13
categories: Snap
tags: Snapcraft
---

Snap(スナップ)パッケージなら、インストールしたいアプリケーションが 他のディストリビューションにあって 自分の使用しているディストリビューションにはない、ということがありません。

Snapパッケージは、特定の Linuxディストリビューション(UbuntuやFedora等)専用パッケージではなく、様々な Linxuディストリビューションにインストールできる パッケージ形式です。
同じファイル [^file] からインストールされます。

現在、20以上の Linuxディストリビューションにインストール可能です。

[^file]: インストール・ファイルはディストリビューションが違っても同じですが、アーキテクチャ(i386 や amd64 等)毎に用意されています。

## snapd が必要

Snapパッケージを利用するには、snapdがインストールされている必要があります。

<https://snapcraft.io/docs/installing-snapd> (公式サイト 英語)

Ubuntuなどには最初からsnapdがインストールされています。  
Lubuntuなどは、Snapパッケージのインストール前に、snapdのインストールが必要です。
Lubuntuの場合、端末で `sudo apt install snapd` とすると snapdを直ぐにインストールできます。

snapdのインストールの参考ページ(Debian, CentOS, openSUSE Leap, Arch Linux)  
<https://gihyo.jp/admin/serial/01/ubuntu-recipe/0582?page=2> (日本語)

## Snapパッケージのインストールとアンインストール

色々なアプリケーションをインストール・アンインストールを繰り返していると、パッケージの依存関係が壊れたり、不要なパッケージが残ることがあります。
しかし、Snapパッケージならそのような事がありません。

Snapパッケージのインストールやアンインストールで、他のインストールされているアプリケーションやパッケージに影響がありません。
Snapパッケージは、他のアプリケーションやライブラリと独立してインストールされるため、他に影響なくアンインストールできます。  
パッケージの依存関係が問題にならないか心配することありません。

## Snapパッケージのインストール方法

Snapパッケージは、
端末からインストールする方法以外に、GUIの Gnomeソフトウエア(gnome-software)やスナップストア(snap-store)や KDE Discover からもインストールできます。

これらでソフトを探すことも出来ます。
まだ公式サイトでも検索できます。  
<https://snapcraft.io/store>

スナップストア(snap-store) そのものがインストールがまだなら `sudo snap install snap-store ` でインストールできます。  
<https://snapcraft.io/docs/installing-snap-store-app>

***
