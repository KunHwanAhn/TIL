# About Vuex
- [Official Page](https://vuex.vuejs.org/kr/)

## 개요
본 문서는 Vuex에 관한 기본적인 개념을 다루는 문서이다.

## Vuex란?
Vuex는 Vue.js 애플리케이션에 대한 상태 관리 패턴 + 라이브러리 입니다. 애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하며 예측 가능한 방식으로 상태를 변경할 수 있습니다.

## Getting Started
[./examples/getting_started.html](./examples/getting_started.html) 참조

## `상태 관리 패턴`이란 무엇인가요?
- 상태: 앱을 작동하는 원본 소스
- 뷰: 상태의 선언적 매핑
- 액션: 뷰에서 사용자 입력에 대해 반응적으로 상태를 바꾸는 방법

```JavaScript
new Vue({
  // 상태
  data() {
    return {
      count: 0
    }
  },
  // 뷰
  template: `<div>{{ count }}</div>`,

  // 액션
  methods: {
    increment() {
      this.count++
    }
  }
})
```

## 상태(State)
- Vuex는 `단일 상태 트리`를 사용한다.
- 각 애플리케이션마다 하나의 저장소만 갖는다.

### Vuex 상태를 Vue 컴포넌트에서 가져오기

#### 계산된 속성(Computed)
Vuex 저장소는 반읒억이기 때문에, 저장소에서 상태를 `검색`하는 가장 간단한 방법은 `계산된 속성(Computed)` 내에서 사태를 가져오는 것이다.

```JavaScript
// Counter 컴포넌트를 만듭니다
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: { // 계산된 속성
    count () {
      return store.state.count
    }
  }
}
```

`store.state.count`가 변경되면 계산된 속성이 변경되고, 관련 DOM 업데이트가 트리거 된다.

> NOTE: 이 패턴은 컴포넌트가 전역 저장소 단독 항목에 의존하게합니다. 모듈 시스템을 사용할 때는 저장소 상태를 사용하는 모든 컴포넌트에서 저장소를 가져와야하며 컴포넌트를 테스트 할 때는 가짜데이터가 필요합니다.

#### 루트 컴포넌트dp 주입 하는 방법
Vuex는 store 옵션(Vue.use(Vuex)에 의해 가능)으로 루트 컴포넌트의 모든 자식 컴포넌트에 저장소를 "주입"하는 메커니즘을 제공합니다.

##### 루트 컴포넌트

```JavaScript
const app = new Vue({
  el: '#app',
  // "store" 옵션을 사용하여 저장소를 제공하십시오.
  // 그러면 모든 하위 컴포넌트에 저장소 인스턴스가 삽입됩니다.
  store,
  components: { Counter },
  template: `
    <div class="app">
      <counter></counter>
    </div>
  `
})
```

##### 자식 컴포넌트

```JavaScript
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return this.$store.state.count
    }
  }
}
```

루트 인스턴스에 store 옵션을 제공함으로써 저장소는 루트의 모든 하위 컴포넌트에 주입되고 `this.$store`로 사용할 수 있습니다.

### `mapState` Helper
[API Reference](https://vuex.vuejs.org/kr/api/#mapstate)

```JavaScript
computed: {
  localComputed () { /* ... */ },
  // 이것을 객체 전개 연산자(Object Spread Operator)를 사용하여 외부 객체에 추가 하십시오.
  ...mapState({
    // ...
  })
}
```

## 변이(Mutation)
- Vuex 저장소에서 실제로 상태를 변경하는 유일한 방법은 변이하는 것입니다.
- 변이에는 `타입` 문자열 `핸들러`가 있습니다.
- 변이는 무조건 `동기적`이어야 합니다.

```JavaScript
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 상태 변이
      state.count++
    }
  }
})
```

### `mapMutaions` Helper
[API Reference](https://vuex.vuejs.org/kr/api/#mapmutations)

```JavaScript
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment' // this.increment()를 this.$store.commit('increment')에 매핑합니다.
    ]),
    ...mapMutations({
      add: 'increment' // this.add()를 this.$store.commit('increment')에 매핑합니다.
    })
  }
}
```

## 액션(Action)
액션은 변이와 유사합니다. 몇가지 다른 점은,
- 상태를 변이시키는 대신 액션으로 변이에 대한 커밋을 합니다.
- 작업에는 임의의 비동기 작업이 포함될 수 있습니다.

```JavaScript
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
})
```

### Example
 비동기 API 호출 과 여러 개의 변이를 커밋 하는 장바구니 결제 예제

 ```JavaScript
 actions: {
  checkout ({ commit, state }, products) {
    // 장바구니에 현재있는 항목을 저장하십시오.
    const savedCartItems = [...state.cart.added]

    // 결제 요청을 보낸 후 장바구니를 비웁니다.
    commit(types.CHECKOUT_REQUEST)

    // 상점 API는 성공 콜백 및 실패 콜백을 받습니다.
    shop.buyProducts(
      products,
      // 요청 성공 핸들러
      () => commit(types.CHECKOUT_SUCCESS),
      // 요청 실패 핸들러
      () => commit(types.CHECKOUT_FAILURE, savedCartItems)
    )
  }
}
 ```

### mapActions Helper
[API Reference](https://vuex.vuejs.org/kr/api/#mapactions)

```JavaScript
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
      'increment' // this.increment()을 this.$store.dispatch('increment')에 매핑
    ]),
    ...mapActions({
      add: 'increment' // this.add()을 this.$store.dispatch('increment')에 매핑
    })
  }
}
```
