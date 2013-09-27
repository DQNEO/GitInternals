# オブジェクトのデータ構造
全てオブジェクトは次のようにして 検証することができます。

* それらのハッシュ値がファイルの中身と一致していること。
* オブジェクトを解凍することができ、解凍したデータは <オブジェクトの種別>  空白  <サイズ> ＋ <byte\0> + <オブジェクトのバイナリデータ> の順番となっていること。

例えばblobであれば、データ構造は下記のようになっている。

blob + " " + size + "\0" + binary_content

## treeオブジェクトの構造

treeオブジェクトは中身の一部がバイナリフォーマットなので、zlib解凍してcatすると画面表示が崩れる。

具体的には、エントリのsha1がバイナリの16進数である。

see http://getpocket.com/a/read/288689326


例
```
blob 12\000hello...
```

## リンク集
* http://git-scm.com/book/ja/Git%E3%81%AE%E5%86%85%E5%81%B4-Git%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88
* http://cdn8.atwikiimg.com/git_jp/pub/git-manual-jp/Documentation/chunked/ch10s02.html
