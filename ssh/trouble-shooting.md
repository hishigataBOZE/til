# トラブルシューティング

## SSH接続が失敗する

※git cloneでssh接続するときも含む

SSH接続の詳細表示で確認する
```bash
$ ssh -vT git@domain.com
```

### 例1 ホスト名が見つからない（解決できない）

```bash
$ ssh -vT git@git.jetbrains.space/hartman
OpenSSH_5.3p1, OpenSSL 1.0.1e-fips 11 Feb 2013
debug1: Reading configuration data /home/igarashi/.ssh/config
debug1: Applying options for git.jetbrains.space/hartman
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Applying options for *
ssh: Could not resolve hostname git.jetbrains.space/hartman: Name or service not known <<< これが原因
```


### 例2 git cloneで`Permission denied (publickey)`

```bash
$ git clone ssh://git@git.jetbrains.space/xxx/xxxx.git xxxxx
Initialized empty Git repository in /var/www/html/xxxxx/.git/
Permission denied (publickey).
fatal: The remote end hung up unexpectedly
```

```bash
$ ssh -vT git@git.jetbrains.space
OpenSSH_5.3p1, OpenSSL 1.0.1e-fips 11 Feb 2013
debug1: Reading configuration data /home/xx/.ssh/config
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Applying options for *
debug1: Connecting to git.jetbrains.space [99.80.164.168] port 22.
debug1: Connection established.
debug1: identity file /home/xx/.ssh/identity type -1 <<< 鍵認証をデフォルトの鍵ファイル名で全部試す。-1は失敗。1が成功
debug1: identity file /home/xx/.ssh/identity-cert type -1
debug1: identity file /home/xx/.ssh/id_rsa type -1
debug1: identity file /home/xx/.ssh/id_rsa-cert type -1
debug1: identity file /home/xx/.ssh/id_dsa type -1
debug1: identity file /home/xx/.ssh/id_dsa-cert type -1
debug1: identity file /home/xx/.ssh/id_ecdsa type -1
debug1: identity file /home/xx/.ssh/id_ecdsa-cert type -1
:
debug1: Trying private key: /home/xx/.ssh/identity
debug1: Trying private key: /home/xx/.ssh/id_rsa
debug1: Trying private key: /home/xx/.ssh/id_dsa
debug1: Trying private key: /home/xx/.ssh/id_ecdsa
debug1: No more authentication methods to try.
Permission denied (publickey).
```

原因は`.ssh/config`でホスト名にパスを指定していたが(Intellij Spaceのサンプル通り)、
ホスト名だけにすると成功した。
予測だが、これが古いバージョンのsshだと解釈できなかったと思われる。

```
# 失敗した設定
Host git.jetbrains.space/hartman <<<
  User git
  HostName git.jetbrains.space/hartman <<<
  PreferredAuthentications publickey
  IdentitiesOnly yes
  IdentityFile ~/.ssh/id_rsa_space
```

```
# 成功した設定
Host git.jetbrains.space <<<
  User git
  HostName git.jetbrains.space <<<
  PreferredAuthentications publickey
  IdentitiesOnly yes
  IdentityFile ~/.ssh/id_rsa_space
```

