# テクニック

## リモートリポジトリの変更

### やったこと

BitBucketからGitHubに移行

### 準備

- ローカルにBitBucketからクローン済み
- GitHubにリポジトリ作成
- ローカルでリモートリポジトリの向き先を変更
```
$ git remote -v
origin	https://hishigataBOZE@bitbucket.org/hishigataBOZE/here-is-bitbucket.git (fetch)
origin	https://hishigataBOZE@bitbucket.org/hishigataBOZE/here-is-bitbucket.git (push)

$ git remote set-url origin https://github.com/hishigataBOZE/here-is-github.git
```

- 変更したリモートリポジトリにpush

```
$ git push

$ git remote -v
origin	https://github.com/hishigataBOZE/here-is-github.git (fetch)
origin	https://github.com/hishigataBOZE/here-is-github.git (push)
```

## 特定ファイルを特定のコミットに戻す

`git checkout [コミット番号] [ファイルパス]`

- 参考：https://qiita.com/ritukiii/items/5bc8f74dbf4dc5d1384c
