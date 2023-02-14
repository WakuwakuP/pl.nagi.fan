# my-pleroma

docker pleroma

## install

### caddy-docker-proxy

<https://github.com/WakuwakuP/dc-caddy-proxy>

```shell
git clone https://github.com/WakuwakuP/dc-caddy-proxy.git
docker network create --driver caddy
docker-compose build
docker-compose up -d
```

### Pleroma起動

```shell
git clone --recursive https://github.com/WakuwakuP/pl.nagi.fan.git
cp .env.esample .env
vi .env
```

```shell
docker network create --driver bridge back-pleroma
./pleroma.sh setup
```

## Update

```shell
./pleroma.sh update
```

## Backup / Restore

```sh
# db backup
docker-compose exec db pg_dump -d pleroma -U pleroma --format=custom -f /pgdump/pleroma.pgdump

# db restore
docker-compose exec db pg_restore -d pleroma -U pleroma -v -1 /pgdump/pleroma.pgdump
```

## ~~update~~ (archived)

```sh
git submodule foreach git pull origin stable
docker-compose build

# build終了まで待つ

docker-compose run --rm web mix ecto.migrate
docker-compose down
docker-compose up -d
```
