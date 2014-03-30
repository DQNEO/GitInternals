# .git/index

http://www8.atwiki.jp/git_jp/pub/Documentation.ja/user-manual.html#the-index

## 豆知識
.git/indexは、削除しても簡単に作り直せる

```shell
rm .git/index
git reset
```

## ファイルの構造


```shell
$ hexdump -C .git/index  |head
 00000000  44 49 52 43 00 00 00 02  00 00 00 c9 53 37 c4 47  |DIRC........S7.G|
 00000010  1b e5 53 25 53 37 c4 47  1b e5 53 25 00 00 fd 00  |..S%S7.G..S%....|
 00000020  01 a8 0c c8 00 00 81 a4  00 00 01 f5 00 00 01 f5  |................|
 00000030  00 00 00 1b 84 01 9b ea  76 a3 72 0e 89 37 54 4a  |........v.r..7TJ|
 00000040  30 23 8e 56 64 57 c5 ce  00 0f 23 2f 31 63 2d 65  |0#.VdW....#/1c-e|
 00000050  6e 74 65 72 70 72 69 73  65 00 00 00 53 37 c4 47  |nterprise...S7.G|
```

```
44 49 52 43 // DIRC
00 00 00 02 // hdr_version
00 00 00 c9 //
```

# 参考
* https://github.com/git/git/blob/master/Documentation/technical/index-format.txt
* ["git indexの中身 - 西尾泰和のはてなダイアリー"](http://d.hatena.ne.jp/nishiohirokazu/20120523/1337766796
) ←一部、正しくない気がする。
