# スクリーンショット

## スクリーンショット画像の影なし設定（デフォルトは影あり）

- 影なし

```
$ defaults write com.apple.screencapture disable-shadow -boolean true
$ killall SystemUIServer
```

- 影あり

```
$ defaults write com.apple.screencapture disable-shadow -boolean false
$ killall SystemUIServer
```

## ファイル名の規則変更設定

- デフォルト
  - ルール： `<prefix> <yyyy-mm-dd> <hh.MM.ss>.<extention>`
  - サンプル： `スクリーンショット 2019-08-01 11.37.43.png`
  
### プレフィックスの設定  

```
$ defaults write com.apple.screencapture name "<prefix>" // 空だとプレフィックスなしになる
$ killall SystemUIServer
```







