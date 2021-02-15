# 30分勉強会

## 目的
- 開発者体験（Developer Experience, DX）の向上
  - 開発時のストレスを減らすこと
- ツールやサービスを理解する
  - すでに知っている人はアンチパターンやユースケースなどを紹介する
  - まだ知らない人は頭の片隅に入れておき、使えそうな時に使っていく
- ツールやサービスそのものの使い方ではなく、それらが実現しようとしている対象について理解を深めるきっかけとする（例: direnv を使うことで環境変数に対する理解を深める）

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

### 議事録
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

### 議事録
- 影響を及ぼすレイヤーを考えて使いこなす
  - シェルの設定ファイル（最上位）
  - direnv（ディレクトリごと）
  - .env（アプリケーションごと）
- 隠避したい内容かどうかを使う基準とする
- 使っている環境変数を一覧するドキュメント的な役割
- Rails の場合、静的な情報は credentials を使うという方法もある

----------

## 第03回 (2021/02/08) Git における「ブランチ」とは？「HEAD」とは？

### 本日の内容
- Git における以下の 2つ の意味を理解する
  - 「ブランチ」
  - 「HEAD」
- Jamboard
  - [30分勉強会 #03「ブランチとは・HEADとは」](https://jamboard.google.com/d/10ZVLS0ZpSI2b4imt6F-5Djake_D03tIoiGbOjvJct0o/viewer?f=0)

### まとめ

#### 「ブランチ（名）」とは
1. 「コミットハッシュ」に貼り付く「名札」のこと
1. 原理上は無くても構わないが、人類にとっては必要
1. 枝分かれしたいずれかの枝の「先頭」に貼り付く

#### 「HEAD」とは
1. 「現在位置」に貼り付く「名札」のこと
1. 「現在位置」は原則「ブランチ」である

#### 「コミット」とは
1. ある時点における「ファイルが保存されているフォルダ」のこと（イメージ）
1. 直前のコミットのコミットハッシュを知っている
1. 例外的なコミットとして「マージコミット」がある

### 所感
- ブランチを「切る」という言い方がとても良くない
  - ブランチを「貼る」「付ける」でいいと思う
  - 他のバージョン管理システムからの名残り？

### 発展
- ブランチを「削除する」とは？
- Git の「タグ」とは？
- push -f をしなければいけないときは、コミットがどういう状態にあるときか？
- rebase や reset の際に必要になる `~`（チルダ）や `^`（キャレット）の意味は？
  - [【やっとわかった！】gitのHEAD^とHEAD~の違い - Qiita](https://qiita.com/chihiro/items/d551c14cb9764454e0b9)

### 議事録
- マージしたときに困ったことになる場合があるが、理由は何だろうか
  - 希望通りのマージができてない（更新されない）
  - 先祖返りすることがある
- `push -f` するときはどういうことが起きているのか
- `git reset --hard` したときにどう戻すか
  - `git checkout コミットハッシュ` や `git reflog` で戻せる
  - 実務的には リモートのコミット（ブランチ）を用いるのが楽
- `detached HEAD` になっても大変なことではない
  - 「ブランチを作成しろ」と言われるが、すぐに既存ブランチに戻るなら作らなくていい
  - ただし、コミットを重ねる場合は、ブランチがないとハッシュしか目印がなくなってしまうので人類には辛い
- 参考記事
  - [GitのHEADとは何者なのか - Qiita](https://qiita.com/ymzk-jp/items/00ff664da60c37458aaa)
  - [【git】git のブランチは「枝」ではない - KaQiita](https://www.kaqiita.com/entry/2018/12/24/222650)

----------

## 第04回 (2021/02/17) Git の rebase (squash) とは？ リモートリポジトリとは？

### 本日の内容
- Git における以下の 2つ の意味を理解する（2つに関連はない）
  - 「rebase (squash)」
  - 「リモートリポジトリ」
- Miro
  - URL

### まとめ

#### 「rebase (squash)」とは
1. `rebase` とは、分岐点の「コミット」のポインタをすげ替える操作のこと
2. `squash` とは、`rebase` の際に同時に行える操作のことで、HEAD から分岐点の「コミット」までを一つにまとめること

#### 「リモートリポジトリ」とは
1. 「ローカル」とは別の場所にあるリポジトリ
2. ローカルリポジトリやリモートリポジトリという名称は、「ブランチ」というラベルに追加で付与される情報に過ぎない

### 所感
- WIP

### 発展
- WIP

### 議事録
- WIP

----------

## 第XX回 (2021/XX/XX) YAMLの闇 について

### 本日の内容
- YAML の闇を探る
- #01、#02 とはスタイルが異なり、何問かの（XX問）問題を提示してそれにひとつひとつ答えを見つけるという形式

### 問題

#### 問題1
ここに問題が入る。ここに問題が入る。ここに問題が入る。ここに問題が入る。ここに問題が入る。ここに問題が入る。ここに問題が入る。ここに問題が入る。ここに問題が入る。ここに問題が入る。ここに問題が入る。

#### 問題1 の解答
ここに解答が入る。ここに解答が入る。ここに解答が入る。ここに解答が入る。ここに解答が入る。ここに解答が入る。ここに解答が入る。ここに解答が入る。ここに解答が入る。ここに解答が入る。ここに解答が入る。

#### 問題1 から分かること
ここに分かることが入る。ここに分かることが入る。ここに分かることが入る。ここに分かることが入る。ここに分かることが入る。ここに分かることが入る。ここに分かることが入る。ここに分かることが入る。

### 発展
ここに発展の内容が入る。ここに発展の内容が入る。ここに発展の内容が入る。ここに発展の内容が入る。ここに発展の内容が入る。ここに発展の内容が入る。ここに発展の内容が入る。

### 議事録
ここに議事録が入る。ここに議事録が入る。ここに議事録が入る。ここに議事録が入る。ここに議事録が入る。ここに議事録が入る。ここに議事録が入る。

# 次回以降のテーマ（予定）
- [ngrok](https://ngrok.com/)
  - serveo
  - localtunnel
  - localhost.run
  - teleconsole
  - pagekite
  - Google Spreadsheet
- [rclone](https://rclone.org/)
  - [rsync](https://rsync.samba.org/documentation.html)
  - scp
- [peco](https://github.com/peco/peco)
- 無限PostgreSQL by Docker
- [ghq](https://github.com/x-motemen/ghq)
- [gh](https://github.com/cli/cli)
- pgcli, mycli
- git rebase (squash, fixup)
- [CircleCI CLI](https://circleci.com/docs/ja/2.0/local-cli/)
  - オレオレ `config.yml` を作る
- [fzf](https://github.com/junegunn/fzf)
- [jq](https://stedolan.github.io/jq/)
  - [yq](https://github.com/kislyuk/yq)
- 30分勉強会を行うための方法
  - [Miro](https://miro.com/)
  - [CommentScreen](https://commentscreen.com/)
  - [slido](https://www.sli.do/jp)
- 個人開発・勉強環境を無料（安価）で構築する
  - GCE の Always Free
  - Heroku
  - Raspberry Pi
  - Netlify
  - Vercel
  - Lightsail
  - ConoHa
  - Dokku (Piku)
  - minio
  - Docker Registry
- 定番 gem の基礎的な使い方
  - Sorcery
  - Runsack
  - Ancestry
  - letter_opener
  - rails-dotenv
  - Bugsnag
  - Shrine
  - Config (Settings)
  - PaperTrail
  - bussiness_time
  - (Materialize)
- 便利ツール
  - DBeaver
  - Metabase
  - Postman
  - Fiddler
  - Wireshark
  - Figma
  - 1Password
  - AltTab
  - Alfred
  - Stream Deck
  - Clipy
  - Magnet
  - Default Folder X
  - Simple URL Copy (Chrome Extension)
