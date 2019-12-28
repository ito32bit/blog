# Snapパッケージ トラブルシューティング

### Snapが 更新後(refresh)、最初の起動でエラーが出る

アイコンをクリックして起動できない時、端末から起動すると エラーを見ることが出きます。

Error: バスエラー (コアダンプ)  
Error: Bus error (core dumped)

回避方法：アンインストールしてから インストールします。  
アンインストールは purge オプションを付けます。
もしアプリケーションが起動中の場合は、終了してから アンインストールします。

端末：
```bash
sudo snap remove --purge スナップ名
sudo snap install スナップ名
```

### Snapが 更新でエラーが出る

Error: cannot perform the following tasks: Fetch and check assertions for snap

回避方法：更新ではなく、アンインストールしてから インストールします。  
アンインストールは purge オプションを付けます。
もしアプリケーションが起動中の場合は、終了してから アンインストールします。

端末：
```bash
sudo snap remove --purge スナップ名
sudo snap install スナップ名
```

なお、これでもエラーになる場合は、再度、アンインストール後に少し時間(５分以上)を待ってからインストールしてみて下さい。

参考: <https://bugs.launchpad.net/snapd/+bug/1844496>  
