# git cat-file -p $object の動きを追う

version:git v1.8.4

## デバグ方法
EmacsでM-x gdb
break parse_sha1_header
run cat-file -p badcafe

## 処理シーケンス
* sha1オブジェクトファイルのヘッダを解析してオブジェクトタイプを決定
* sha1オブジェクトファイルのボディ部分を読み出し

## blobファイルのヘッダ解析
```
#0  parse_sha1_header (hdr=0x7fffffffd240 "blob 12", sizep=0x7fffffffd270) at sha1_file.c:1620
#1  0x00000000004e8d2a in sha1_loose_object_info (sha1=0x7fffffffe610 ";\030\345\022ۧ\236L\203", oi=0x7fffffffd2c0) at sha1_file.c:2506
#2  sha1_object_info_extended (sha1=0x7fffffffe610 ";\030\345\022ۧ\236L\203", oi=0x7fffffffd2c0) at sha1_file.c:2538
#3  0x00000000004e8f7d in sha1_object_info (sha1=<value optimized out>, sizep=<value optimized out>) at sha1_file.c:2573
#4  0x0000000000416fa2 in cat_one_file (argc=<value optimized out>, argv=<value optimized out>, prefix=<value optimized out>) at builtin/cat-file.c:49
#5  cmd_cat_file (argc=<value optimized out>, argv=<value optimized out>, prefix=<value optimized out>) at builtin/cat-file.c:396
#6  0x0000000000404bf7 in run_builtin (argc=3, argv=0x7fffffffe920) at git.c:303
#7  handle_internal_command (argc=3, argv=0x7fffffffe920) at git.c:466
#8  0x0000000000404e22 in run_argv (argc=3, av=<value optimized out>) at git.c:512
#9  main (argc=3, av=<value optimized out>) at git.c:595
```


