<template>
  <div id="app">
    <h1>Look at this file tree:</h1>
    <tree-wrapper
      :item="filesData"
    />
  </div>
</template>

<script>
import TreeWrapper from './components/TreeWrapper.vue'
import filesData from '../public/static/node_modules.json'

export default {
  name: 'App',
  components: {
    TreeWrapper
  },
  data() {
    return {
      filesData
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
