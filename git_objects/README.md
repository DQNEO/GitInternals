# Git Objectsのサンプル


```
$ git cat-file -p HEAD:git_objects/texts
100644 blob 9eefe7f84dc57d24f2ffb411f86a2a43d7ca2562    bocchan.txt
100644 blob ce013625030ba8dba906f756967f9e9ca394464a    hello.txt
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad    helloworld.txt
```

下記のテキストファイルとバイナリファイルの相互変換ができれば、Gitのloose objectの実装ができたと言える。

* texts/hello.txt <=> ce/0136....
* texts/bocchan.txt <=> 9e/ef7....

