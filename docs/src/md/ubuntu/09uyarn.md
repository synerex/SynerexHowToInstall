# YARNのインストール

 YARN（Yet Another Resource Negotiator）とは、NPMの高速版パッケージのようなもの

## YARNインストール済み確認

 ターミナルから以下のコマンドを実行し、バージョンが正しく表示されることを確認する。

```
$ yarn --version
```

 バージョン表示で失敗する場合、以下インストールを実施する。

## YARNインストール
YARN未インストール時、ターミナルから以下のコマンドを実行し、インストールを実施する。

- リポジトリのGPGキーをインポート


```
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
```

- Yarn APTリポジトリをシステムのソフトウェアリポジトリリストに追加


```
$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```

- パッケージリストを更新してYarnをインストール


```
$ sudo apt update
$ sudo apt install yarn
```

前項「YARNインストール済み確認」に従い、バージョンが正しく表示されることを確認する。

