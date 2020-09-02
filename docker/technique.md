# テクニック

## Dockerfileで親ディレクトリのファイルを参照する方法

ファイル構成
```
$ tree -L 3
.
├── docker
│   └── web
│       ├── Dockerfile
│       └── php.ini
└── docker-compose.yml
```

```
// Dockerfile
：
# web/php設定ファイル
COPY docker/web/php.ini /etc/php.ini
```

### Dockerfileの場合

```
// ビルド時のパスを指定
$ cd /Users/{username}/workspace/projectA/docker/web/
$ docker build /Users/{username}/workspace/projectA/docker/web/ -f ./Dockerfile
```

### docker-composeの場合

```
# docker-compose.yml
version: '3'
services:
  web:
    build:
      context: ./
      dockerfile: ./docker/web/Dockerfile
    ports:
      - "80:80"
    volumes:
      - ./:/var/www/html/app:cached
    privileged: true
```

## コンテナが自動起動をdocker-compose.ymlを変更せずに停止する

### 停止したいコンテナIDを控える

```
% docker container ls -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS                     PORTS               NAMES
84b104d073fd        nginx:1.17-perl       "nginx -g 'daemon of…"   44 hours ago        Exited (0) 7 minutes ago                       web
d0d97808df02        sys_php               "docker-php-entrypoi…"   44 hours ago        Exited (0) 7 minutes ago                       phpfpm
658bc8fb1be2        mysql:5.7             "docker-entrypoint.s…"   44 hours ago        Exited (0) 7 minutes ago                       db2_1
ad8eac30766a        mysql:5.7             "docker-entrypoint.s…"   44 hours ago        Exited (0) 7 minutes ago                       db4_1
d096e8c86778        mysql:5.7             "docker-entrypoint.s…"   44 hours ago        Exited (0) 7 minutes ago                       db1_1
7c40ff9c84ae        mysql:5.7             "docker-entrypoint.s…"   44 hours ago        Exited (0) 7 minutes ago                       db
832967db05c3        mysql:5.7             "docker-entrypoint.s…"   44 hours ago        Exited (0) 7 minutes ago                       db3_1
13332e2cb610        mysql:5.7             "docker-entrypoint.s…"   44 hours ago        Exited (0) 7 minutes ago                       db5_1
```

### 自動起動を停止

#### コマンド

`docker update --restart=no <MY-CONTAINER-ID>`

`<MY-CONTAINER-ID>`に控えたコンテナIDを指定

コンテナIDをまとめて指定も可能
```
% docker update --restart=no 832967db05c3 13332e2cb610 d096e8c86778 ad8eac30766a 658bc8fb1be2
832967db05c3
13332e2cb610
d096e8c86778
ad8eac30766a
658bc8fb1be2
```

#### dockerを再起動して自動起動していないかを確認
