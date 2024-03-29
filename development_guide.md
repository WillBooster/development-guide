# 開発ガイド

本文書では、WillBoosterに新たに参加した開発者向けの案内をまとめます。

## はじめに

全プロジェクトで[Git](https://git-scm.com/)を使用しています。
使用した経験がない方は、使い方をあらかじめ学習しておいてください。

多くのプロジェクトで、主に次の言語、フレームワークを採用しています。
入門記事やチュートリアルを読み、ある程度の理解を得てから開発に臨むと、開発を円滑に進められます。

- [TypeScript](https://www.typescriptlang.org/)
- [React](https://ja.react.dev/)
- [Next.js](https://nextjs.org/)
- [Prisma](https://www.prisma.io/)

## 開発環境

[開発入門](introduction_to_development.md)を参照してください。

## 動作確認

ほとんどのプロジェクトでは、以下の共通コマンドで基本的な動作確認を行えるようになっています。
例外もあるため、動作しない場合はプロジェクト管理者に問い合わせてください。

次のコマンドで、開発モードでのアプリケーションの実行を開始できます。
結果を見るには、ブラウザで http://localhost:3000 を開いてください。

```sh
yarn start
```

アプリケーションを初めて実行する場合などには、あらかじめ次のコマンドを実行しておいてください。
シードデータには動作確認用のユーザも含まれており、`db/seeds/index.ts`に記述されたユーザ名とパスワードでサインインできるようになります。

```sh
# 依存パッケージをインストールする。
yarn

# データベースを初期化する。
yarn db-reset
```

次のコマンドで Prisma Studio を起動すると、データベースの状態を手軽に確認できます。

```sh
yarn run prisma studio
```

次のコマンドでテストを実行できます。

```sh
yarn test
```

## 開発フロー

WillBooster では、タスクを GitHub の issues で管理しています。
社内の開発者が、各 issue の assignees を設定することでタスクを割り振ります。

1. 最新のソースコードを取得して、最新の DB スキーマを反映する
   ```
   git pull
   yarn db-migrate
   ```
2. GitHub の issues からアサイン済みの issue を確認する
   - アサイン済みの issue がない場合など、未アサインの issue に着手したい場合は、 Code Owners から許可を得ること。
   - Code Owners は issue が枯渇していることに気づきにくいので、積極的に声をかけること 💪。
3. 着手する issue を 1 つ決めて、該当 issue 専用のブランチを作成する
   - ブランチの命名規則に明確なルールはありませんが、特にこだわりがなければ、 `<issue番号>-<変更内容を端的に表現する語句>` （e.g. `34-problems-page`） を推奨します。
   - e.g. `git switch -c 34-problems-page`
4. 何らかの変更を加えてコミットする
   - ステップ 7 のように PR タイトルの書き方にはルールがありますが、コミットメッセージの書き方にはルールがありません。
   - コミットの粒度も自由ですが、細かく記録しておいたほうが、巻き戻しが容易になって安心です。
   - e.g. `git add -A && git commit -m "Implementing problems page"`
   - Linter のエラーを解決できずにコミットできない場合は、 `--no-verify` を追加してください。
5. 完成前であっても、作成したブランチをリモートリポジトリ(GitHub)にプッシュする
   - e.g. `git push origin 34-problems-page`
   - 型エラーを解決できずにプッシュできない場合は、 `--no-verify` を追加してください。
     - フレームワークのコード生成を実行していないことが原因のケースもあるため `yarn gen-code` も試してください。
6. GitHub 上で該当ブランチの Pull request (PR) を作成する。
   - 早期に PR を作っていただくと、他の開発者が助言を与えやすくなります。
7. PR のタイトルを [Conventional Commits](https://www.conventionalcommits.org/ja/v1.0.0/) に準拠させる。
   - PR のタイトルの先頭に、機能追加・改良の場合は `feat:` 、バグ修正の場合は `fix:` 、テストの追加・改良・修正の場合は `test:` などを追記します。
   - PR のタイトルが `main` ブランチにマージした時のコミットメッセージになります。
   - Squash & Merge でマージするため、一つ一つのコミットは Conventional Commits に従う必要はありません。（従っても構いません。）
   - 未完成、作業中ならば PR のタイトルの先頭にさらに `[WIP] ` を追記します。
     - 例. `[WIP] feat: implement the problems page`
8. 変更・コミット・プッシュを繰り返す
9. 完成したら、他の開発者にレビューをリクエストする。
   - PR のタイトルに `[WIP] ` が付いていれば削除する。
   - PR に `review requested` ラベルを付与する。
   - Code Owners 以外の、類似タスクに従事する開発者 1 名をレビュアにアサインする。候補者がいなければ Code Owners の 1 名をアサインする。
   - PR のコメント欄で、Code Owners 全員とレビュアにアサインした 1 名に向けたメンションを付けて、レビューを依頼する旨をコメントする。
10. レビュアーから指摘を受けたら、変更・コミット・プッシュを行う
11. 指摘への対応が終わったら、再レビューを依頼する（依頼方法は下図を参考にすること）
    ![image](https://user-images.githubusercontent.com/436237/152084294-0f0b332d-2f75-4daf-b7e4-2b3ab8d61333.png)
12. Code Owners から Approve を受けたら該当 issue は完了
13. Code Owners から指示をされた場合のみ PR をマージする。指示がなければマージしない。
    - プロジェクトの進行上、マージを遅らせたいケースがあるためです。

## Q&A

### データベースのバックアップ方法（社内の開発者のみ）

1. Bitwarden から`gcp-sa-key.json (<プロジェクト名>)`の添付ファイルをダウンロードします。
2. このリポジトリのルートディレクトリに、1 でダウンロードしたファイルを`gcp-sa-key.json`にリネームし、配置します。
3. `WB_ENV={stagingまたはproduction} yarn db-restore` コマンドを実行してバックアップを取得します。
   - バックアップファイルは`db/restored.sqlite3` に生成されます。すでに同名のファイルが存在する場合、上書きされるので注意してください。

## トラブルシューティング

### http://localhost:3000 を開けない。

この説明は以下の条件に当てはまる人を対象にしています。

- **WSL2 を使用していてメモリ制限をしている。**  
  WSL のメモリを制限しすぎているため動作が非常に遅くなっている可能性があります。以下の手順を試してみてください。
  1. システムリソースを表示して WSL の使用メモリを確認する。WSL の使用メモリが制限したメモリとほぼ同じ値になっていない場合、メモリの制限が原因ではありません。
  2. メモリを制限している wslconfig ファイルの設定を変更し WSL の制限メモリサイズを大きくする。

### 変更を`pull`した後などに、特に問題ないはずのコードで型エラーが出る

以下のコマンドを実行してみてください。

```
yarn gen-code
```
