# my-pleroma

docker pleroma

## install

### caddy-docker-proxy

既に導入済みの場合はスキップしてよい

<https://github.com/WakuwakuP/dc-caddy-proxy>

#### caddy-docker-proxy のdocker-composeを用意

```shell
git clone https://github.com/WakuwakuP/dc-caddy-proxy.git
```

#### caddy-docker-proxy に必要な docker network を作成

```
docker network create --driver caddy
```

#### caddy-docker-proxy ビルド

```
docker-compose build
```

#### caddy-docker-proxy 立ち上げ

```
docker-compose up -d
```

### Pleroma起動

#### 構築用コードを取得

```shell
git clone --recursive https://github.com/WakuwakuP/pl.nagi.fan.git
```

#### 環境変数ファイルをサンプルからコピー

```shell
cp .env.esample .env
```

#### 環境変数ファイルを環境にあわせて修正

```shell
vi .env
```

#### 必要な docker network を作成

```shell
docker network create --driver bridge back-pleroma
```

#### 初回セットアップ

```shell
./pleroma.sh setup
```

## Update

### 基本的なアップデート

```shell
./pleroma.sh update
```

### 必要に応じて段階的に実行する

#### 最新の構築用コードを取得

```shell
./pleroma.sh update-code
```

#### イメージを更新

```shell
./pleroma.sh update-image
```

#### コンテナを新しく作り直してマイグレーション

```shell
./pleroma.sh update-container
```

## Backup / Restore

### backup

```shell
docker-compose exec db pg_dump -d pleroma -U pleroma --format=custom -f /pgdump/pleroma.pgdump
```

### restore

```shell
docker-compose exec db pg_restore -d pleroma -U pleroma -v -1 /pgdump/pleroma.pgdump
```
