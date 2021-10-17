# nginx-proxy + acme-companion
Docker Composeでnginx-proxyとacme-companionを起動するためのリポジトリです。  
`nginx-proxy`ネットワークにコンテナを追加すると、そのコンテナに対して自動でリバースプロキシを構築し、SSL/TLSに対応させます。

単体で使う物ではなく、基本的には他のコンテナと連携させて使用します。

## 必要動作環境
- Docker `>= 19.03.0`
- Docker Compose `>= 1.27.0`

参考: [Compose ファイル - Docker ドキュメント](https://matsuand.github.io/docs.docker.jp.onthefly/compose/compose-file/)

## 使用方法
基本的な流れとしては、まず本リポジトリのDocker Composeを起動して、それから本来の接続先となるコンテナを起動、`nginx-proxy`ネットワークに追加します。

### nginx-proxyとacme-companionの起動
```bash
$ docker-compose up -d
```

### リバースプロキシの対象となるコンテナの起動
リバースプロキシの対象となるコンテナの環境変数に以下を含めると、自動でリバースプロキシを構築します。  
他にも色々な設定がありますがここでは最低限必要な物を記載しますので、詳しくは参考を参照してください。

- `VIRTUAL_HOST`: このコンテナに対応するホスト名
- `LETSENCRYPT_HOST`: SSL/TLS対応させるホスト名(基本的には`VIRTUAL_HOST`と同じ)
- `LETSENCRYPT_EMAIL`: SSL/TLSの証明書の期限が切れそうな場合に連絡が来るメールアドレス

#### WordPressの例
[kthksgy/docker-compose-wordpress](https://github.com/kthksgy/docker-compose-wordpress)を参照してください。  
このリポジトリと組み合わせて使用するWordPressのリポジトリです。

## 参考
### Docker Hub
[nginxproxy/nginx-proxy](https://hub.docker.com/r/nginxproxy/nginx-proxy)
[nginxproxy/acme-companion](https://hub.docker.com/r/nginxproxy/acme-companion)
