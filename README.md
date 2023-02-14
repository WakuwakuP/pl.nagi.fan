# pl.nagi.fan

Environment construction script of [pl.nagi.fan](https://pl.nagi.fan)

emojis and themes, terms-of-service.html, etc. are in [pl.nagi.fan-custom](https://github.com/WakuwakuP/pl.nagi.fan-custom).

## install

### caddy-docker-proxy

Skip if you have already installed

<https://github.com/WakuwakuP/dc-caddy-proxy>

#### Get the code for caddy-docker-proxy

```shell
git clone https://github.com/WakuwakuP/dc-caddy-proxy.git
```

#### Create docker network required for caddy-docker-proxy

```
docker network create --driver caddy
```

#### Build caddy-docker-proxy

```
docker-compose build
```

#### start caddy-docker-proxy

```
docker-compose up -d
```

### Pleroma起動

#### Get the code for pl.nagi.fan

```shell
git clone --recursive https://github.com/WakuwakuP/pl.nagi.fan.git
```

#### Copy the .env.example to .env

```shell
cp .env.esample .env
```

#### Modify .env according to the environment

```shell
vi .env
```

#### Create the required docker network

```shell
docker network create --driver bridge back-pleroma
```

#### First setup

```shell
./pleroma.sh setup
```

## Update

### Basic update

```shell
./pleroma.sh update
```

### Gradually update as needed

#### Get the latest building code

```shell
./pleroma.sh update-code
```

#### Update docker image

```shell
./pleroma.sh update-image
```

#### Create a new container and database migrate

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
