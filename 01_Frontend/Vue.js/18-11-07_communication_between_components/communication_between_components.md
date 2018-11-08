# Communication between components
- [Official Document](https://vuejs.org/v2/guide/components.html)
- [Reference](https://flaviocopes.com/vue-components-communication/)

## 개요
본 문서는 Vue.js에서 Component간 통신 방법에 대해 정리한 문서이다.

## Way to communicate between components
- props
- Events from child to parent
- Event bus
- Vuex

## props
부모 Component에서 자식 Component에게 데이터를 전달하는 방법이다.

``` HTML
<template>
  <div>
    <Car color="green" />
  </div>
</template>

<script>
import Car from './components/Car'

export default {
  name: 'App',
  components: {
    Car
  }
}
</script>
```

## Events from child to parent
자식 Component에서 부모 Component에게 데이터 또는 상태 변화를 전달하는 방법이다.

### Parent

``` HTML
<template>
  <div>
    <Car v-on:clickedSomething="handleClickInParent" />
  </div>
</template>

<script>
export default {
  name: 'App',
  methods: {
    handleClickInParent: function(param1, param2) {
      //...
    }
  }
}
</script>
```

### Child

``` HTML
<script>
export default {
  name: 'Car',
  methods: {
    handleClick: function() {
      this.$emit('clickedSomething', param1, param2)
    }
  }
}
</script>
```

## Event bus
부모 Component와 자식 Component 사이에 Event Bus Object를 공유하여 통신하는 방법이다.

### Parent

``` HTML
<template>
  <div>
    <Car event-bus="eventBus" />
  </div>
</template>

<script>
import Vue from 'vue'

export default {
  name: 'App',
  data: function () {
    return {
      eventBus: new Vue()
    }
  },
  methods: {
    doSomthing: function(param1, param2) {
      this.eventBus.$emit('doSomething', param1, param2)
    }
  }
}
</script>
```

### Child

``` HTML
<script>
export default {
  name: 'Car',
  props: [
    eventBus: {
      type: Object
    }
  ],
  mounted() {
    this.eventBus.$on('doSomething', (param1, param2) => {
      // Do something
    })
  }
}
</script>
```

## Vuex
[Vuex](https://vuex.vuejs.org/)를 사용하는 방법이다.
