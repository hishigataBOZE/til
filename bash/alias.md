# エイリアス設定

## 設定方法

```
// 設定を書くファイル
$ vi ~/.bashrc
// 即時反映
$ source ~/.bashrc
```

## エイリアス記述（引数なし）

```bash
# list
alias ll="ls -la"
```

## エイリアス記述（引数あり）

```bash
# git svn add (like: git add)
function gitsvn() {
    command git add $1 && git commit -m $2
}
```

### 使い方
```bash
$ gitsvn "path/to/file"  "commit message"
```



