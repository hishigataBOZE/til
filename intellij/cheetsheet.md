# チートシート

## 画像ファイルからimgタグ生成

###　やり方

1. Projectから画像ファイルを選択（複数可）
2. コピー（Cmd+c）
3. 貼り付け対象のファイルでペースト（Cmd+v）
4. 文字置換（Cmd+r）
- 置換前： `^(.*\.(jpg|png))$\n^(.*\.(jpg|png))$` |
- 置換後： `<picture>\n  <source media="(max-width: 480px)" srcset="<?php path_image(); ?>$3" width="1170" height="1000">\n  <img src="<?php path_image(); ?>$1" alt="" width="1920" height="800">\n</picture>` |

### before/after

- before

```
text01.png
text01_sp.png
text02.png
text02_sp.png
text03.png
text03_sp.png
icon_02.png
icon__sp.png
```

- after
```html
<picture>
 <source media="(max-width: 480px)" srcset="<?php path_image(); ?>  text01_sp.png" width="1170" height="1000">
 <img src="<?php path_image(); ?>  text01.png" alt="" width="1920" height="800">
</picture>
<picture>
 <source media="(max-width: 480px)" srcset="<?php path_image(); ?>  text02_sp.png" width="1170" height="1000">
 <img src="<?php path_image(); ?>  text02.png" alt="" width="1920" height="800">
</picture>
<picture>
 <source media="(max-width: 480px)" srcset="<?php path_image(); ?>  text03_sp.png" width="1170" height="1000">
 <img src="<?php path_image(); ?>  text03.png" alt="" width="1920" height="800">
</picture>
<picture>
 <source media="(max-width: 480px)" srcset="<?php path_image(); ?>  icon__sp.png" width="1170" height="1000">
 <img src="<?php path_image(); ?>  icon_02.png" alt="" width="1920" height="800">
</picture>
```
