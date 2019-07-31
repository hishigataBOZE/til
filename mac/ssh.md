# SSH

## ワーニングが表示されてSSH接続できない

```
$ ssh target-server
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for '/xxxx/private_key.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/xxxx/private_key.pem": bad permissions
sshuser@114.514.19.19: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```

- 原因：鍵のパーミッションが所有者の読み取り専用でない

- 対処方法
```
$ chown 0400 /xxxx/private_key.pem
```

