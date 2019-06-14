# その他

## 実行エラー時の対応

 「go run」「go build」等、実行時にパッケージなしエラーになる場合は、前項「関連パッケージのインストール」の他に、個別でパッケージをインストールすることも可能。

 【エラー例】※Windows画面（Ubuntuでは類似画面となる）

![](../../img/ubuntu/u07msc01.png)

 内容：「github.com/spf13/viper」パッケージが見つからない

 【対策コマンド】

```
$ go get -u github.com/spf13/viper
```

## go generateエラー

 go generateでエラーになる要因として、goパッケージの未インストール、パス不正の場合があるので、パスが正常に通っているか確認する。

 Protocのパス定義でinclude部分を参照する部品があるが、パス不正により、エラーとなる例があった。（Protocパスの設定見直しにて解決）。


## go buildエラー

 go buildでエラーになる要因として、go.modに問題がある場合があるので、内容が正しいことを確認する。

「go mod init」で初期化する方法でも対応可能。（前章「自動ダウンロードする場合【サンプル2】」参照※）

 ※モジュールバージョン管理の更新に注意

「go mod init」で初期化していても、ローカルフォルダへの相対参照設定がされていないことが原因で「go build」「go mod tidy」等でパッケージ無エラーになる場合がある。「go.mod」に以下内容を手入力で追記することでエラーが解消することがある。

(追記内容は相対参照設定の一例であり、取込む際には適宜調整のこと)

```mod:go.mod
replace (
   github.com/synerex/synerex_alpha/api => ../../../api
   github.com/synerex/synerex_alpha/api/adservice => ../../../api/adservice
   github.com/synerex/synerex_alpha/api/common => ../../../api/common
   github.com/synerex/synerex_alpha/api/fleet => ../../../api/fleet
   github.com/synerex/synerex_alpha/api/library => ../../../api/library
   github.com/synerex/synerex_alpha/api/ptransit => ../../../api/ptransit
   github.com/synerex/synerex_alpha/api/rideshare => ../../../api/rideshare
   github.com/synerex/synerex_alpha/api/routing => ../../../api/routing
   github.com/synerex/synerex_alpha/nodeapi => ../../../nodeapi
   github.com/synerex/synerex_alpha/sxutil => ../../../sxutil
)
```



― 以上 ―
