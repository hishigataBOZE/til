# ワンライナー

## hostsファイルに追記

`sudo sh -c "echo '127.0.0.1 xxx.local' >> /private/etc/hosts"`

- アカウント個別のhostsファイル：`/private/etc/hosts`
- sudo実行が必要な場合、`-c`オプションをつけ、ダブルクォーテーションで実行コマンドをくくる
- キャッシュリセット`sudo killall -HUP mDNSResponder`
