# 俺式 設定変更

## Finderの日本語表記ディレクトリを英語に変更

1. ワンライナー 
```
$ rm ~/Applications/.localized \
~/Desktop/.localized \
~/Documents/.localized \
~/Downloads/.localized \
~/Movies/.localized \
~/Music/.localized \
~/Pictures/.localized \
~/Public/.localized
```
2. Finder再起動（コマンド`killall Finder`）

- 注意： Mojave、High Sierra（10.13.6）で確認済み。以前のバージョンだとやり方が異なるかも
- 参考： https://qiita.com/ppworks/items/8cb15dcc5ff587964112

