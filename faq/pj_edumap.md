# Edumap

### `vagrant provision --provision-with app-install`でエラー`Logging into ghcr.io for user WillBooster-bot failed`が発生する

コンテナ`data-mng-01`のファイル`/etc/systemd/resolved.conf`に`DNS=8.8.8.8 8.8.4.4`を設定する。

ホストで：

```sh
vagrant ssh
```

コンテナ`edumap-lxd`で：

```sh
container-data-mng-01
```

コンテナ`data-mng-01`で：

```sh
sudo vim /etc/systemd/resolved.conf
sudo systemctl restart systemd-resolved.service
```

#### 参照

- https://discord.com/channels/896895021138214952/896897451049517060/1242020919363244153

### コンテナ`app-d-02-nc4`でマイグレーションを実行したい

```sh
/var/www/app/Edumap2/bin/cake nc4.migrations all
```

サブコマンド（上記では`all`）の詳細はドキュメントの[5.7. マイグレーション](https://github.com/NC-4/docs/wiki/5.7.-%E3%83%9E%E3%82%A4%E3%82%B0%E3%83%AC%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3)で示されている。
