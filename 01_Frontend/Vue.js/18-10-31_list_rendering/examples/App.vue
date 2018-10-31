<template>
  <div>
    <div>From App.vue</div>
    <list-rendering></list-rendering>
  </div>
</template>

<script>
import ListRendering from './components/ListRendering.vue'

export default {
  name: 'app',
  components: {
    ListRendering
  }
}
</script>

<style>

</style>
