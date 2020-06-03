<template>
  <div id="app">
    <search></search>
  </div>
</template>

<script>
let d = []
for (let i = 0; i < 1000; i++) {
  d.push({ id: i, value: i })
}
export default {
  name: 'app',
  components: {
    Search: () => import('@/components/LoadImage.vue')
  },
  data() {
    return {
      data: d
    }
  }
}
</script>

<style scoped lang="scss">
#app {
  height: 100%;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
