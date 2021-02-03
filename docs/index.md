# 30分勉強会

## 目的
- 開発者体験（Developer Experience, DX）の向上
  - 開発時のストレスを減らすこと
- ツールやサービスを理解する
  - すでに知っている人はアンチパターンやユースケースなどを紹介する
  - まだ知らない人は頭の片隅に入れておき、使えそうな時に使っていく

## 内容
- 30分
  - 5分で説明
  - 25分で質疑やハンズオン

# 各回

## 第01回 (2021/01/25) .git/info/exclude について

### 何ができるようになるか？
- Git で「自分だけが」追跡されたくないファイルを指定することができるようになる
  - `.gitignore` の自分専用版

### どうやるか？
- 各リポジトリ配下の `.git/info/exclude` に追跡されたくないファイル名を書く
  - 正規表現を用いることができる

### 何が嬉しいか？
- 自分だけのスクリプトやコードを誤ってコミットしなくて済む
  - テストや開発のために書いた一時的なコード
    - `my_test.rb`
    - `filterMethodTest.js`
  - エディタや導入しているツール特有の設定ファイル
    - `.idea/`
    - `.vscode/`
    - `.envrc`

### 発展
- `.git/hooks` についても調べてみよう
  - `overcommit` や `husky` も調べてみよう

### 質疑時間に話されたこと
- 常に無視することが決まっているファイルは `~/.gitignore` に書くと手間が減る
- `git update-index --assume-unchanged` や `git update-index --skip-worktree` と組み合わせて使う
  - [git の監視から逃れる方法 - Qiita](https://qiita.com/sqrtxx/items/38a506e59df67cd5d3a1)
  - 落とし穴もあるので注意する
- `dotfiles` の利用
  - コマンドエイリアスを定義する
- ユースケースがいまいち思いつかない

----------

## 第02回 (2021/02/03) direnv について

### 何ができるようになるか？
- ディレクトリごとに環境変数を追加することができるようになる

### どうやるか？
- [インストールする](https://github.com/direnv/direnv/blob/master/docs/installation.md)
  - パッケージマネージャ経由でよい
- `eval "$(direnv hook zsh)"` を `.zshrc` などに書いてコマンドを実行可能にする
- 環境変数を追加したいディレクトリで `$ direnv edit .` を実行する
- `.envrc` ファイルが編集状態になるため、環境変数を書き込む
- `$ direnv allow` を実行し、`.envrc` を有効化することで適用完了

### 何が嬉しいか？
- 例: エディタを使い分けられる
  - `EDITOR=hogehoge`
    - nano
    - Micro
    - Vim
    - Emacs
- ディレクトリに置くことで、そのディレクトリで用いる環境変数を明確に示すことができる

### ポイント
- 環境変数が複数の場所で定義されていた場合、どれが優先（上書き）されるのか？
  - [source_up](https://direnv.net/man/direnv-stdlib.1.html)

### 発展事項
- dotenv (.env) との共存
- `$ direnv edit` の場合の挙動（`.` をつけない場合）は？
- 上書きではなく追記するにはどうしたらよいか？
- 既存の `.envrc` を自前のエディタ経由で（`$ direnv` コマンドを経由しないで）編集した場合はどうなるか？
- `cross-env` とは？
- [公式ドキュメント](https://direnv.net/man/direnv-stdlib.1.html)

# 次回以降のテーマ（予定）
- ngrok
  - serveo
  - localtunnel
  - localhost.run
  - teleconsole
  - pagekite
  - Google Spreadsheet
- rclone
  - rsync
  - scp
- peco
- YAMLの闇
- 無限PostgreSQL
- ghq, gh
