# 30分勉強会

## 目的
- 開発者体験（Developer Experience, DX）の向上
  - 開発時のストレスを減らすこと

## 方法
- 30分
  - 5分で説明
  - 25分で質疑やハンズオン

# 各回

## 第01回 (2021/01/25) .git/info/exclude について

### 何を実現するためのものか？
- Git で「自分だけが」追跡されたくないファイルを指定することができる
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

### 質疑時間に話されたこと
- 常に無視することが決まっているファイルは `~/.gitgnore` に書くと手間が減る
- `git update-index --assume-unchanged` や `git update-index --skip-worktree` と組み合わせて使う
  - [git の監視から逃れる方法 - Qiita](https://qiita.com/sqrtxx/items/38a506e59df67cd5d3a1)
  - 落とし穴もあるので注意する
- `dotfiles` の利用
  - コマンドエイリアスを定義する
- ユースケースがいまいち思いつかない
