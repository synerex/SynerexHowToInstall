# gRPCのインストール

 gRPCは、RPC (Remote Procedure Call)を実現するためにGoogleが開発したプロトコルの1つである。

 Protocol Buffersを使ってデータをシリアライズし、高速な通信を実現できる点が特長である。

 gRPCでは、IDL（インターフェース定義言語）を使ってあらかじめAPI仕様を.protoファイルとして定義し、そこからサーバー側＆クライアント側に必要なソースコードのひな形を生成する。

 言語に依存しないIDLで先にインタフェースを定義することで、様々なプログラミング言語の実装を生成できるというメリットがある。

## gRPCインストール済み確認

 以下いずれかのフォルダ内に「genproto＊」「grpc＊」フォルダがあればOK

 $GOPATH/src/google.golang.org

 $GOPATH/pkg/mod/google.golang.org

 【確認例】

```
$ ls $GOPATH/src/google.golang.org
$ ls $GOPATH/pkg/mod/google.golang.org
```

 フォルダが存在しない場合、以下インストールを実施する。

## gRPCインストール

 ターミナルから以下のコマンドを実行する。

```
$ go get -u google.golang.org/grpc
```

 ※処理に数分程度要することがあるので気長に待つ。

 処理終了後、前項「gRPCインストール済み確認」に従い、フォルダがあることを確認する。

