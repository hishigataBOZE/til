# gem

## トラブルシューティング

### install error (High Sierra)

```bash
$ sudo gem install jekyll
:
:
ld: symbol(s) not found for architecture i386
clang: error: linker command failed with exit code 1 (use -v to see invocation)
make[3]: *** [libffi.la] Error 1
make[2]: *** [all-recursive] Error 1
make[1]: *** [all] Error 2
make: *** ["/Library/Ruby/Gems/2.3.0/gems/ffi-1.11.1/ext/ffi_c"/libffi-i386/.libs/libffi_convenience.a] Error 2

make failed, exit code 2

Gem files will remain installed in /Library/Ruby/Gems/2.3.0/gems/ffi-1.11.1 for inspection.
Results logged to /Library/Ruby/Gems/2.3.0/extensions/universal-darwin-17/2.3.0/ffi-1.11.1/gem_make.out
```

#### 解決方法

```bash
$ brew install automake autoconf libtool
$ sudo gem install ffi -v '1.9.21'
```
ffiのインストールに失敗するので、手動でインストールするよう。

#### 参考 
- https://github.com/ffi/ffi/issues/611#issuecomment-364621532
