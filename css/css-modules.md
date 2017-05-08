# CSS modulesについて

## what
ref. [CSSモジュール ― 明るい未来へようこそ](http://postd.cc/css-modules/)

Reactとかでjsx単位でcssをスコープして使えるようにしようという概念的なもの  
SMACCSとかBEMとかのような、CSS設計手法の話ではない  
  
モジュール内で閉じるので、BEMの`button--active`みたいな書き方がそもそも不要になる。  
`active``disabled`みたいな状態クラスを発行する。  


## how
```
* components/submit-button.js */
import styles from './submit-button.css';
 
buttonElem.outerHTML = `<button class=${styles.normal}>Submit</button>`
```

jsにimportしてコンパイルするとスタンドアロンなファイルが生成される。

### 命名規則
```
/* components/submit-button.css */
.normal { /* all styles for Normal */ }
.disabled { /* all styles for Disabled */ }
.error { /* all styles for Error */ }
.inProgress { /* all styles for In Progress */
```

クラスが全てのスタイルを記述されている必要がある。  
`button is-error`のように、基本スタイル+オーバーライドスタイルの組み合わせではなく、`error`が基本スタイルも含めて全て持つ必要がある。

### コンポジション
構成。組み立て。(ref.https://dictionary.goo.ne.jp/jn/84116/meaning/m0u/)

```
.common {
  /* all the common styles you want */
}
.normal {
  composes: common;
  /* anything that only applies to Normal */
}
.disabled {
  composes: common;
  /* anything that only applies to Disabled */
}
.error {
  composes: common;
  /* anything that only applies to Error */
}
.inProgress {
  composes: common;
  /* anything that only applies to In Progress */
}
```

要はSassのextend的なことができる。吐き出され方は違う。
Sassではこうすることで１クラスに統合している。
```
.Button--common, .Button--normal, .Button--error {
  /* font-sizes, padding, border-radius */
}
.Button--normal {
  /* blue color, light blue background */
}
.Button--error {
  /* red color, light red background */
}
```

CSS Modulesは、共通クラスを抽象化、差分は差分で別クラスにし、js側でどのクラスを付与するのか取捨選択する。なので、DOMにレンダリングされるときはマルチクラスで書き出される。
```
.components_submit_button__common__abc5436 { /* font-sizes, padding, border-radius */ }
.components_submit_button__normal__def6547 { /* blue color, light blue background */ }
.components_submit_button__error__1638bcd { /* red color, light red background */ }

```

```
styles: {
  common: "components_submit_button__common__abc5436",
  normal: "components_submit_button__common__abc5436 components_submit_button__normal__def6547",
  error: "components_submit_button__common__abc5436 components_submit_button__error__1638bcd"
}
```





