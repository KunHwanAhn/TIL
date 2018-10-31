# About List Rendering on Vue.js
- [Official Document](https://kr.vuejs.org/v2/guide/list.html)

## 개요
본 문서는 Vue.js에서 `v-for`를 이용하여 List Rendering을 하는 법에 대한 문서 이다.

## v-for
angualr.js의 `ng-repeat`에 대응하는 Directive. ng-repeat처럼 Array 뿐만 아니라, Object도 처리할 수 있다.

> Vue.js v2.2.0 이상에서는 `v-bind:key`가 필수로 필요하니 주의!

### Array case
- 1st Parameter: Array Data
- 2nd Parameter: Data Index

### Object case
- 1st Parameter: Object Value
- 2nd Parameter: Object Key

> Object의 경우, 객체 반복 순서는 Object.keys()의 키 나열 순서에 따라 걸정되며, JavaScript 엔진 구현에 의존적이니 주의!

### 예시

#### HTML
``` HTML
<ul id="example-2">
  <li v-for="(item, index) in items" :key="index">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

#### JavaSscript

``` js
var example2 = new Vue({
  el: '#example-2',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```
