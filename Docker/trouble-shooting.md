# トラブルシューティング

## ボリュームマウントしたら、ビルド時に配置したファイルが消える現象

#### ソースファイル＋Dockerfileの構成

```
- ローカル
source
├── app <<<<< ソース関係
├── docker <<<<< Docker関係
|   ├── .env
|   ├── php.ini
|   └── Dockerfile
└── docker-compose.yml
```

#### ビルド時の作業の一部
- 「.env」を「/home/user/」配下にコピー
-  「php.ini」を「/etc/」配下にコピー

#### ビルド直後Docker内

```
/
├── home
|   └── user
|       └── .env
└── etc
    └── php.ini
```

#### ボリュームマウントしないとき

```
/
├── home
|   └── user
|       └── .env <<<<< 存在する
└── etc
    └── php.ini
```


#### 「source」を「/home/user/」配下にボリュームマウント時

```
/
├── home/user/.env
|   └── user <<<<< マウントしたディレクトリで上書きされる
|       ├── app
|       ├── docker
|       |   ├── .env
|       |   ├── php.ini
|       |   └── Dockerfile
|       └── docker-compose.yml
└── etc
    └── php.ini
```

### 「消える」というよりは、コンテナ内のディレクトリはマウントしたディレクトリが優先されるよう

「docker-compose.yml」で「volume」をコメントアウトして起動すると「.env」は存在する
```
# docker-compose.yml
    volumes:
      - ./:/home/md_stg:cached
```
