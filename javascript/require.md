ref.http://qiita.com/uryyyyyyy/items/b10b012703b5396ded5a

ref.https://www.slideshare.net/terurou/common-js

## why
よく見るしなんとなく使ってるけどなんなのという

## what
そもそもJavaScriptはブラウザ上で動かすための言語として発達したもので、サーバサイドで同行する仕組みがなかった。
そのため、commonJSという仕様で策定された。

簡単に言うと、JavaSctiptをモジュール化して別のjsファイルで読み込んだりできるって言う感じ。

これがない場合、外に定義したものを別のjsファイルで使いたいときはscriptタグ内に書いてグローバルにしておくとかするしかなかった。

## サンプル
`exports`オブジェクトにいれると別ファイルか`require`して使うことができる。

```calc.js
exports.add = function (x,y){
  return x + y;
}

var minus = function(x,y) {
  return x - y;
}
```

```main.js
var calc = require('calc');

calc.add(1,2); // 3
calc.minus(5,1) // ReferenceError
```
