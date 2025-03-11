# Kintoneへ転送するリバプロ

**本コンテナは、検証するためのものです。**

## 検証

リバプロでFormBridgeの公開フォームアクセスする。

http://0e80ac6c.example.com/public/cd81ae5de982ed6dfdd854684299d35315043e5ef95dd27a2dc6dd888c8cda40
       <--[A]-> <---[B]--->        <-------------------------[C]---------------------------------->

    [A]: Formbridgeのサブドメイン(有料版で変更可能)
    [B]: プロキシドメイン
    [C]: FormID

リバプロのサブドメインをFormBridgeのサブドメインと一致させることで動作する。
ただし、最終的に FormBridge のURLにリダイレクトされる。上記のURLなら以下にリダイレクトされる

https://0e80ac6c.form.kintoneapp.com/public/cd81ae5de982ed6dfdd854684299d35315043e5ef95dd27a2dc6dd888c8cda39

## 必要なもの

- mkcert
- Docker
  - Docker Compose v2 プラグイン

## 動かしかた

### サーバ側

1. Docker 及び、Docker Compose v2 プラグインをインストールします。
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


### クライアント側

1. `hosts`ファイルに、 `サーバのIP     [A].example.com` を追加する。
1. certs/mkecert-nokey.p12 を 信頼するRoot証明書にインポートする。
1. Webブラウザを起動し、`https://[A].example.com`にアクセスする。


