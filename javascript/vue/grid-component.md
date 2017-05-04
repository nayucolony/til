## ソート

## やりたいこと
- 表の項目名の矢印アイコンをクリックすると、昇順、降順が切り替わる。
  - `Name`をクリックするとアルファベット順に並び替わる
  - `Power`をクリックすると数値大小順に並び替わる
- 矢印アイコンの向きも連動して変わる

## 流れ
* 1.モデルの定義
  - 状態は昇順か降順。1か-1でよさそうー。
* 2.コントローラーの定義
  - どうやってモデルを書き換える？
* 3.ビューに反映

## データのイニシャライズ

昇順or降順にする機能をつける。
モデルとして昇順のときは1、降順のときは-1をとり、それを切り替えるだけでいいみたいな作りにする。

```
data: function () {
  var sortOrders = {}
  this.columns.forEach(function (key) {
    sortOrders[key] = 1
  })
  return {
    sortKey: '',
    sortOrders: sortOrders
  }
}
```

forEachは配列の要素それぞれに適用
`this.columns`は`gridColumns`を受け取っていて`['name', 'power']`という配列。
sortOrdersという空配列を定義しておいて、columnsの要素それぞれをキーとし、その値を１とする。

`{name:1,power:1}`みたいな感じになる。


### 1.sortByメソッドを呼び出す
引数に「key」を渡す。
このkeyはcolumnsの要素一つ一つが該当するので、`name`か`power`のどっちかになる。

#### 1-1.sortKeyにkeyを渡す
this.sortKeyすなわりdataオプションのsortKeyに`name`or`power`を代入
    
#### 1-2.sortOrders[]にkeyを渡す
`this.sortOrders[key] = this.sortOrders[key] * -1`

`this.sortOrders[name] = this.sortOrders[name] * -1`

`this.sortOrders`はオブジェクトで、デフォルトは`{name:1,power:1}`になっている
sortByメソッドが実行されるとkeyに該当するほうの値がひっくり返る。1だったら-1とか。
これが別のところに影響して実際に中身がひっくり返る。

### 2.フィルタする
```
filteredData: function () {
  var sortKey = this.sortKey // name or power
  var filterKey = this.filterKey && this.filterKey.toLowerCase()
  var order = this.sortOrders[sortKey] || 1
  var data = this.data
  if (sortKey) {
  console.log(data);
    data = data.slice().sort(function (a, b) {
      a = a[sortKey]
      b = b[sortKey]
      return (a === b ? 0 : a > b ? 1 : -1) * order
    })
  }
```

引数なしの`slice()`で配列コピーできる
コピーした配列に対してソートを適用し、data変数に格納。
引数a,bはそれぞれ

```
{ name: 'Chuck Norris', power: Infinity },
{ name: 'Bruce Lee', power: 9000 },
{ name: 'Jackie Chan', power: 7000 },
{ name: 'Jet Li', power: 8000 }
```
`Chuck Norris`と`Bruce Lee` =>`Bruce Lee`が下
`Bruce Lee`と`Jackie chan` =>`Bruce Lee`が下

ここで`Chuck Norris`と`Jackie chan`の順番がわからないので決める => `Chuck Norris`が下

現時点で`Jackie chan,Chuck Norris,Bruce Lee`の並び

`Bruce Lee`と`Jet Li`を比べる => `Bruce Lee`が下

`Jet Li`のいち付を決める。遡る順番で比較していく

`Jet Li`と`Chuck Norris` => `Chuck Norris`が下
`Jet Li`と`Jackie Chan` => `Jackie Chan`が下

`Jackie chan,Jet Li,Chuck Norris,Bruce Lee`

### なんでコピーするん

ref.https://codepen.io/nayucolony/pen/PmKaEa
ソートは破壊的メソッドで、もともとの配列の中身を書き換えてしまう。

`data = data.slice().sort()`とすることで、コピーした配列を書き換えて格納できるので、元の配列が壊れない。

### order
`var order = this.sortOrders[sortKey] || 1`は値として1 or -1 をとる。
|| 1




### 例えば、sortKeyがnameだった場合
```
a=a[name]
b=b[name]
```
みたいになる。

