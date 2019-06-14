# 関連パッケージのインストール

 Synerex Alphaのインストール例と関連パッケージのインストール方法を記述する。インストール要否を判断し作業を行うこと。

## Synerex Alphaインストール

 コマンドプロンプトから以下のコマンドを実行し、Synerex Alphaをインストールする。

 ※以下はインストール例であるため、適宜調整する

```
【サンプル1】
> mkdir c:\MyProjects
> cd c:\MyProjects
> git clone https://github.com/synerex/synerex_alpha

【サンプル2】
> go get -u github.com/synerex/synerex_alpha    ← %GOPATH%\src 配下へコピーする
```

| 【 Synerexリポジトリ例】          |
| --------------------------------- |
| github.com/synerex/synerex\_alpha |
| 上記フォーク先                    |



## 関連パッケージのインストール（参考）

 Synerex Alphaを実行するためには、関連パッケージのインストールが必要となる。

 通常は、go buildで関連パッケージを自動でダウンロードするが、go version 1.12以降では、go modulesパッケージ仕様が変更され、ビルド対象パッケージが %GOPATH%\src 配下にある場合、デフォルトでは関連パッケージのダウンロードがされない。

 そのため、モジュールが見つからない旨のエラーが発生する場合は、go build前に以下コマンド実行するか、手動にて関連パッケージをインストールする必要がある。

### ダウンロード先

| ダウンロード種別 | ダウンロード先                                               |
| ---------------- | ------------------------------------------------------------ |
| 自動             | %GOPATH%\pkg\mod（%GOPATH%\srcにないモジュールを自動ダウンロード） |
| 手動             | %GOPATH\src                                                  |



### 自動ダウンロードする場合

 Synerex Alphaが動作するために必要な関連パッケージを自動インストールする。
（ビルド対象パッケージが %GOPATH%\src 配下に無い場合は不要）

  go buildコマンド発行前に、コマンドプロンプトから以下のコマンドを実行するか、環境変数「GO111MODULE」を設定する。

```
> set GO111MODULE=on
```

 以下buildサンプル

```
【サンプル1】
> cd %GOPATH%\src\github.com\synerex\synerex_alpha\cli\daemon
> set GO111MODULE=on
> go build               ← 正常終了すると「se-daemon.exe」が生成される 
> se-daemon build

【サンプル2】
> cd %GOPATH%\src\github.com\synerex\synerex_alpha\cli\daemon
> set GO111MODULE=on
> go mod init se-daemon  ← 正常終了すると「go.mod」が生成される
> go mod tidy            ← 正常終了すると「go.sum」が生成される
> go build               ← 正常終了すると「se-daemon.exe」が生成される 
```

 上記でビルドエラーになる場合は次項「手動ダウンロードする場合」を実行することで解決する場合がある。

 ※環境変数にて「GO111MODULE」を設定する方法については省略する。


### 手動ダウンロードする場合

 Synerex Alphaが動作するために必要な全関連パッケージを手動インストールする。

 コマンドプロンプトから以下のコマンドを実行する。

```
 【Synerex Alphaディレクトリ例】：%GOPATH%\src\github.com\synerex\synerex_alpha

> cd [Synerex Alphaディレクトリ]
> go get ./...
```

 ※1 ダウンロードに時間がかかるため気長に待つ。

 ※2 GO111MODULE=autoに伴うエラーが発生する場合は、前項「自動ダウンロードする場合」同様にsetコマンドにて対応する。

