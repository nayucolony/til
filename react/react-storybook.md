# React-storybook

## why
大規模サービスのコンポーネントガイドに

## what
jsxファイルからコンポーネントガイドを作れる

- 導入
- 記法


## 導入
### インストール
```
yarn add storybook
```

### 起動
```
yarn run start-storybook
```

http://localhost:6006
にアクセス

### サンプル
今から作る

## 書き方

### 流れ
- ストーリーを作る
- 状態を追加する


### storiesOf
`storiesOf('汎用ボタン',module)`
- 第一引数はメニューに表示されるラベルテキスト
- 第二引数の`module` is 何

使うときは
```
import { storiesOf } from '@kadira/storybook';
```
すること。

### .add()
`.add('アイコン付き',function)`
storiesOfにメソッドチェーンして書く。モジュールの状態を追加できる。
- 第一引数はメニューに表示されるラベルテキスト
- 第二引数はコンポーネントを返す関数

#### example

```
import React from 'react';
import { storiesOf, action } from '@kadira/storybook';

storiesOf('Button', module)
  .add('with a text', () => (
    <button>My First Button</button>
  ))
  .add('with no text', () => (
    <button></button>
  ));
```
    




