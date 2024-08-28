# FAQ Edumap

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
