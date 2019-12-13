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
