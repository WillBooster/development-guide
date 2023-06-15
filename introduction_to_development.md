# 開発入門

社内の開発者のサポートを受けやすいMac、次点でLinux（Ubuntu）上での開発を推奨します。
Windowsをご利用の方は、Windows Subsystem for Linux 2（WSL2）上での開発を推奨します。

1. [Windows Subsystem for Linux 2 (WSL2)](https://docs.microsoft.com/ja-jp/windows/wsl/install-win10)を有効にする。
2. WSL2上にUbuntuをインストールする。
   - Windows StoreでいくつかのUbuntuイメージが提供されていますが、バージョン番号が記載されていないものは最新版になるのでおすすめです。

## 環境構築

[Git](https://git-scm.com/)をインストールしてください。
使用した経験がない方は、使い方をあらかじめ学習しておいてください。

以降の項目については、初めからすべてをセットアップしておく必要はありません。
開発対象のプロジェクトの採用技術に対応する節のみを参照してください。

### Node.js + Yarn

概要

- [asdf](https://github.com/asdf-vm/asdf)で以下のツールをインストールする。
  - [Node.js](https://nodejs.org/ja/)
  - [Yarn](https://yarnpkg.com/)

#### Windows (WSL) / Linux (Ubuntu)

1. 基本的な開発用のパッケージをインストールする。
   - `sudo apt update && sudo apt install -y build-essential`
2. `asdf`の依存パッケージをインストールする。
   - `sudo apt update && sudo apt install -y curl git dirmngr gpg gawk`
   - cf. http://asdf-vm.com/guide/getting-started.html#_1-install-dependencies
   - cf. http://asdf-vm.com/guide/getting-started.html#plugin-dependencies
3. `asdf`をインストールする。
   - `git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.10.2`
   - cf. http://asdf-vm.com/guide/getting-started.html#_2-download-asdf
4. 「全プラットフォーム共通」の手順に進む。

#### Mac OS

1. Homebrewをインストールする。
   - `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
   - cf. https://brew.sh/
2. `asdf`をインストールする。
   - `brew install asdf`
   - cf. http://asdf-vm.com/guide/getting-started.html#_2-download-asdf
3. 「全プラットフォーム共通」の手順に進む。

#### 全プラットフォーム共通

1. `asdf`にパスを通す。
   - http://asdf-vm.com/guide/getting-started.html#_3-install-asdf の手順に従う。
2. 端末を再起動して、`asdf --version`コマンドが動作することを確認する。
3. `asdf`にNode.jsとYarnのプラグインを追加する。
   - `asdf plugin add nodejs; asdf plugin add yarn`
4. Node.jsをインストールして、システム全体で使用するバージョンを指定する。
   - `asdf list all nodejs; asdf install nodejs lts; asdf global nodejs lts`
5. Yarnをインストールして、システム全体で使用するバージョンを指定する。
   - `asdf install yarn $(npm show yarn version); asdf global yarn $(npm show yarn version)`
6. `asdf`の設定を変更する。
   - `echo 'legacy_version_file = yes' > ~/.asdfrc`
   - cf. http://asdf-vm.com/guide/getting-started.html#using-existing-tool-version-files
7. プロジェクトが要求するツール群を`asdf`でインストールする。
   ```
   cd <プロジェクトのルートディレクトリパス>
   asdf install
   ```
