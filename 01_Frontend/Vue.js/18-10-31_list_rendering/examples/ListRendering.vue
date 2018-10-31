<template>
  <div>
    <div>From ListRendering.vue</div>

    <div>
      <div>Rendered List</div>
      <ul>
        <li v-for="(data, index) in renderingList" :key="index">
          <div>{{ index }} || {{ data.text }}</div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      renderingList: []
    }
  },
  created() {
    this.renderingList = [
      { text: '1st'},
      { text: '2nd'},
      { text: '3rd'}
    ];
  }
}
</script>

<style scoped>

</style>
