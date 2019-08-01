# 俺式 設定変更

## Finderの日本語表記ディレクトリを英語に変更

### こんなに楽になる

- ターミナルで英語のタブ補完が効く

### 設定方法

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

## キーのリピートを短くする

### こんなに楽になる

- ターミナルで矢印キーの移動を素早く

### 設定方法

1. 「システム環境設定」の「キーボード」を開く
  1.1. 「キーのリピート」を「速い」に調整  
  1.1. 「リピート入力認識までの時間」を「短い」に調整

- 参考： https://men-bou.net/mac_keyrepeat_max/
