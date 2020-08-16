---
title: Snapパッケージのトラブルシューティング
date: 2019-12-28 00:00:00
updated: 2020-08-16
categories: Snap説明
tags: Snap作成 トラブルシューティング
---

Snapのインストール時や更新後にエラーが出ることがあります。その時の対応策です。

## snapが 起動しない エラー Fontconfig warning

エラー例:  
```bash
$ qterminal-snap
Fontconfig warning: FcPattern object weight does not accept value [40 210)
Segmentation fault (コアダンプ)
```

この様なエラーが出た場合は次のコマンドを試してみます。  
```bash
fc-cache -r
sudo fc-cache -r
```

これで改善しない場合は次のコマンドを試してみます。  
```bash
rm ~/.cache/fontconfig/*
sudo rm /var/cache/fontconfig/*
```

## Snapが 更新後(refresh)、最初の起動でエラーが出る

アイコンをクリックして起動できない時、端末から起動すると エラー内容を見ることが出きます。

Error: `バスエラー (コアダンプ)`  
Error: `Bus error (core dumped)`

回避方法：アンインストールしてから インストールします。  
アンインストールは purge オプションを付けます。
（注意：そのアプリケーションの設定メニューなどで変更した内容は消えて初期状態に戻ります）
もしアプリケーションが起動中の場合は、終了してから アンインストールします。

```bash
sudo snap remove --purge スナップ名
sudo snap install スナップ名
```

## Snapが エラーが出て更新できない

Error 例: `cannot perform the following tasks: Fetch and check assertions for snap`

回避方法：更新ではなく、先にアンインストールしてから インストールします。  
アンインストールは purge オプションを付けます。
（注意：そのアプリケーションの設定メニューなどで変更した内容は消えて初期状態に戻ります）
もしアプリケーションが起動中の場合は、終了してから アンインストールします。

```bash
sudo snap remove --purge スナップ名
sudo snap install スナップ名
```

なお、これでもエラーになる場合は、再度、アンインストール後に少し時間(５分以上)を待ってからインストールします。

関連: <https://bugs.launchpad.net/snapd/+bug/1844496>  

## snapコマンドが エラー cannot communicate with server

エラー例:  
```bash
$ snap list
error: cannot communicate with server: Post http://localhost/v2/snaps:
 dial unix /run/snapd.socket: connect: connection refused
```

この様なエラーが出た場合は次のコマンドを試してみます。  
```bash
sudo systemctl restart snapd.service
```

***
