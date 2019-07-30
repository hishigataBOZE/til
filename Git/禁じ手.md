# 禁じ手

## Git HistoryのCommitter・Authorを一括改変

### ケース

他の人のマシン借りてコード直したとき、git pushまでしちゃったとき

### やり方
```Shell
$ git filter-branch -f --commit-filter '
        if [ "$GIT_AUTHOR_EMAIL" = "検索条件" ]; # 検索条件。他にも書き方はある
        then
                GIT_AUTHOR_NAME="i_am_author";
                GIT_AUTHOR_EMAIL="i_am_author@email.address";
                GIT_COMMITTER_NAME='i_am_committer';
                GIT_COMMITTER_EMAIL='i_am_committer@email.address'
                git commit-tree "$@";
        else
                git commit-tree "$@";
        fi' HEAD

$ git push -f # 強制プッシュ
```

### 参考： 

- 1コミットだけ改変： https://yuzu441.hateblo.jp/entry/2016/06/29/214535
- Committer・Authorの違い： http://kz-engineer-scrap.hatenablog.com/entry/2016/04/05/032916
