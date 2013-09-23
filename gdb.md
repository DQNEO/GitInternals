# GDBの使い方
* makeするときにデバグオプションを付ける(make -d)
* 基本はEmacsからM-x gdb

## gdbの詳細な使い方
実行する
```
run cat-file -p badcafe
```

### ブレークポイントを設置、表示、削除
関数を指定してブレークポイントを設置
```
break main
```
ソースファイルと行番号を指定してブレークポイントを設置
```
break hoge.c:123
```
ブレークポイントの一覧を表示
```
info break
```
設置したブレークポイントを削除
```
delete 2 4
```

## デバグ中の操作
* s,step 関数の中に入る (ステップイン)
* n,next 関数の中に入らずに次へ (ステップオーバー)
* finish 関数から抜ける (ステップアウト)
* c,continue 再開

## 参考
* [Gitのソースコードでも読もうかな。準備編 - デバッガ - そんなこと覚えてない](http://blog.eiel.info/blog/2012/12/22/ready-to-read-source-git/)