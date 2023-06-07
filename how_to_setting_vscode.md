プログラムを執筆するソフトウェア、統合開発環境はさまざま存在するが、この記事ではMicrosoft社のVisual Studio Codeというアプリケーション（以下、VS Codeと記述）をインストールし、初期設定を行う手順を記す。

# VS Codeのインストール

## ダウンロード

ダウンロードは[こちら](https://code.visualstudio.com/)
"Download {Version}"のようなボタン（たとえば"Download Mac Universal", "Download for Windows"など）を押下するとOSに対応したソフトウェアがダウンロードされる。（アクセスしているPCのOSと異なるバージョンが表示された場合は、その右側にある"∨"マークをクリックして対応したバージョンを選択する。）

## インストール

ダウンロードが終了した後は、ファイルを開き、インストーラを起動する。OSにより操作方法は異なるが、手順は標準的な他のソフトウェアと同様である。Windowsの場合、インストール時にさまざまなオプションが表示されるが、"PATHへの追加"というオプションは有効にすることをオススメする。有効にした場合、Shell環境にて`$ code {targetFile}`とすると目的のファイルをVS Codeで開くことが可能になる。

# 拡張機能のインストール

VS Codeでは拡張機能をインストールすることにより、便利な機能を使うことができる。WillBooster社のプロジェクトではESLintとPrettierというコード整形ツールを使用しているが、VS Codeの拡張機能でそれに対応したものをインストールすることにより、半自動でフォーマットを実行することができる。

VS Codeの拡張機能は、Visual StudioのMarketplaceから該当商品ページの"Install"ボタン押下 -> "Visual Studio Codeを開く"か、VS Code内部の拡張機能タブで該当拡張機能を検索 -> "Install"の2通りの方法がある。お好みの方法で構わない。

## prettier

Prettierをインストールする。
ダウンロードは[こちら](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## eslint

ESLintをインストールする。
ダウンロードは[こちら](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

# 設定

VS Code左下の歯車マークをクリックし、"Settings"メニューから設定画面を開ける。

"Search settings"とある検索欄に"onsave"と入力すると出てくる、"Format On Save"にチェックを入れる。
"Search settings"とある検索欄に"formatter"と入力すると出てくる、"Default Formatter"を"Prettier"にする。

こうすることで、Ctrl-S(Cmd-S)での保存時に自動でフォーマットが行われるようになる。

# 番外編

## 日本語化拡張

Japanese Language Packをインストールする。
ダウンロードは[こちら](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-ja)

適用には再起動が必要。

## オートセーブ

設定での"Files: Auto Save"を"afterDelay"とすると、オートセーブとなる。ただし、その場合前述の"Format On Save"は動作しなくなる。

## フォント

VS Codeデフォルトのフォントは、お世辞にもプログラミング向けとは言い難い。等幅フォントに変更をオススメする。筆者は[UDEV Gothic](https://github.com/yuru7/udev-gothic)が最近のお気に入り。全角スペースが入ってしまったときに気付きやすいという特徴がある。(全角スペースの対処だけならVSCodeの拡張にもありますので、お好みで。)


## その他オススメ拡張

### 見た目系
- [indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow) : インデントを色別で見やすくしてくれる

- [errorlens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens) : エラー表示が見やすくなる。エラーメッセージがマウスホバーしなくても見えるようになる。

- [code-spell-checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) : 変数等に含まれるアルファベット文字列に、英単語として存在しないスペルがあった場合にハイライトしてくれる

### 言語系

- [Prisma](https://marketplace.visualstudio.com/items?itemName=Prisma.prisma) : Prisma

- [JavaScript and TypeScript Nightly](https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv) : TypeScirpt
