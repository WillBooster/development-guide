# Prisma

### マイグレーションファイルを生成したいが実行してほしくない。

```sh
DATABASE_URL="file:./dev.sqlite3?connection_limit=1" yarn prisma migrate dev --create-only
```

`DATABASE_URL`に設定すべき値は開発対象アプリケーションの`.env.development`などから入手できる。
