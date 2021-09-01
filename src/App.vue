<template>
  <div id="app">
    <Content/>
  </div>
</template>

<script>

import Content from './components/content/index.vue'
export default {
  name: 'App',
  components: {
    Content
  }
}
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  display: block;
}
</style>
