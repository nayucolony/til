# 論理演算子||の特殊な使い方

ref.http://qiita.com/Imamotty/items/bc659569239379dded55

## 経緯

https://jsfiddle.net/nayucolony/xkkbfL3L/878/ において

`var order = this.sortOrders[sortKey] || 1`という記述があったので調べた。


## TL;DR
- 右辺を初期値として指定できる

## 解説

（まず前提を補足すると、プログラム上では、左辺の`this.sortOrders[sortKey]`は`1`か`-1`の数値をとる。）

使用を確認すると以下のように買いてあった。
ref.https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Logical_Operators

```
expr1 を true と見ることができる場合は、expr1 を返します。
そうでない場合は、expr2 を返します。
したがって、真偽値と共に使われた場合、 演算対象のどちらかが true ならば、|| は、true を返し、両方とも false の場合は、false を返します。
```

つまり、左辺の`this.sortOrders[sortKey]`が引数が渡されてない場合などはfalseになるので、`order`が右辺の値をとることになる。

falseになるものについては以下のとおり
```
false と見ることができる式の例は、null、0、空文字列 ("")、あるいは、undefined と評価されるものです。
```
要は、（意図的に0を返したりしていない場合）値を取るべき変数が値を取ってない = 未定義である場合などにfalseになり右辺が採用されるので
右辺は「初期値」として扱える。
