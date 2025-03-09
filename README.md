# Kintoneへ転送するリバプロ

**本コンテナは、検証するためのものです。**

## 検証結果

リバプロに別URLをKintoneへ転送する設定しても、それを経由する通信は、Kintoneで本来のURLへリダイレクトされてしまうため、意味がない。

## 必要なもの

- mkcert
- Docker
- Docker Compose

## 動かしかた

1. Docker Compose をインストールします。
1. `mkcert`をインストールします。

   - `CAROOT=$(pwd)/CA mkcert -install` を実行して、自己中間証明書をシステムにインストールします。

1. 本リポジトリをクローンして、 vi等のテキストエディタで`ngine.conf`の修正箇所を編集する。
   ```
   git clone https://path/to/kintone_revproxy.git
   cd kintone_revproxy
   vi nginx.conf
   ```
1. `docker compose up`でコンテナを起動する。
   ```
   docker compose up
   ```
1. `hosts`ファイルに、 `127.0.0.1     example.com` を追加する。
1. Webブラウザを起動し、`https://example.com`にアクセスする。


