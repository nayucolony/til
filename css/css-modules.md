# CSS modulesについて

## what
ref. [CSSモジュール ― 明るい未来へようこそ](http://postd.cc/css-modules/)

Reactとかでjsx単位でcssをスコープして使えるようにしようという概念的なもの  
SMACCSとかBEMとかのような、CSS設計手法の話ではない  
  
モジュール内で閉じるので、BEMの`button--active`みたいな書き方がそもそも不要になる。
`active``disabled`みたいな状態クラスを発行して


## how
```
* components/submit-button.js */
import styles from './submit-button.css';
 
buttonElem.outerHTML = `<button class=${styles.normal}>Submit</button>`
```

jsにimportしてコンパイルするとスタンドアロンなファイルが生成される。
