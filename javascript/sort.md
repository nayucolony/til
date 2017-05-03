ref. https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

## 概要

配列の要素をソートできるメソッド

## 構文

```
array.sort(compareFunction);
```

## 引数

### compareFunction
ソート順を定義する関数を指定します。
省略された場合、配列は各要素の文字列比較に基づき辞書順にソートされます。

#### 辞書順にソートとは
たとえば80と9だと、数的なソートでは9が先。
でも辞書だと80が先。
