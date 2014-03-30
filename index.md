# .git/indexの解説

* .git/indexは、"ステージング/インデックス"情報を保持してるバイナリファイルである。
* 中身を表示するには`git ls-files --stage`

## ファイルの構造

例として"minigit"プロジェクトの.git/indexをとりあげる
```shell
$ git clone git://github.com/DQNEO/minigit.git
$ cd minigit
$ git checkout
```

`git ls-files --stage`で中身を表示できる
```
$ git ls-files --stage | head
100644 95ba71b8e7c2d70965d9a5086a9fabd58e87d259 0       .gitignore
100644 960a0c393e5e493e911ac24ac42d6eb125409263 0       Makefile
100644 9d7f6b8213c452a8e698ccb5557cdf5d36ccf25c 0       README.md
100644 0392373249530f848adca4413ed159a6cde3887e 0       c_samples/is_substr.c
100644 b439e0a12503c7744ed2fb8da7dd3bf1a541acae 0       c_samples/parse_git_index.c
```

`hexdump -C`で生のバイナリデータを見れる
```shell
$ hexdump -C .git/index  | head
00000000  44 49 52 43 00 00 00 02  00 00 00 29 53 32 25 dd  |DIRC.......)S2%.|
00000010  1c 22 62 97 53 32 25 dd  1c 22 62 97 00 00 fd 00  |."b.S2%.."b.....|
00000020  01 a4 07 e1 00 00 81 a4  00 00 01 f5 00 00 00 00  |................|
00000030  00 00 00 71 95 ba 71 b8  e7 c2 d7 09 65 d9 a5 08  |...q..q.....e...|
00000040  6a 9f ab d5 8e 87 d2 59  00 0a 2e 67 69 74 69 67  |j......Y...gitig|
00000050  6e 6f 72 65 00 00 00 00  00 00 00 00 53 32 25 dd  |nore........S2%.|
00000060  1c 22 62 97 53 32 25 dd  1c 22 62 97 00 00 fd 00  |."b.S2%.."b.....|
00000070  01 a4 07 e2 00 00 81 a4  00 00 01 f5 00 00 00 00  |................|
00000080  00 00 00 b5 96 0a 0c 39  3e 5e 49 3e 91 1a c2 4a  |.......9>^I>...J|
00000090  c4 2d 6e b1 25 40 92 63  00 08 4d 61 6b 65 66 69  |.-n.%@.c..Makefi|```
```

* ファイルの中身はヘッダ部とボディ部からなりたっている。
* ヘッダ部は固定長12バイト
* ボディ部はエントリの連続体になっている。
* エントリとは、ファイル1個を表す情報である。

```
// ヘッダー
44 49 52 43 // シグネチャ("DIRC")
00 00 00 02 // ヘッダのバージョン (=2)
00 00 00 29 // エントリ数 0x29 (=41個)
// ここから各エントリ
// ここからファイル".gitignore"の情報
53 32 25 dd // ctime sec
1c 22 62 97 // ctime nano sec
53 32 25 dd // m_time sec
1c 22 62 97 // m_time nano sec
00 00 fd 00 // dev
01 a4 07 e1 // inode
00 00 81 a4 // mode (=100644)
00 00 01 f5 // uid (=501)
00 00 00 00 // guid (=0)
00 00 00 71 // size (=27)
95 ba 71 b8  e7 c2 d7 09 65 d9 a5 08 6a 9f ab d5 8e 87 d2 59 // sha1
00 0a       // namelen (=10 ".gitignore"は10文字)
2e 67 69 74 69 67 6e 6f 72 65 // ".gitignore"
00 00 00 00  00 00 00 00 // zero padding
// ここからファイル"Makefile"の情報
53 32 25 dd // ctime sec
以下、同じように続く
```

## 壊れたときの対処法
 まれに壊れることがあるが、簡単に作り直せる
```shell
rm .git/index
git reset
```

# 参考
* https://github.com/git/git/blob/master/Documentation/technical/index-format.txt
* http://www8.atwiki.jp/git_jp/pub/Documentation.ja/user-manual.html#the-index

