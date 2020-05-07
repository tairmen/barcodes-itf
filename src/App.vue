<template>
  <div id="app">
    <barcodes/>
  </div>
</template>

<script>
import barcodes from './components/barcodes.vue'

export default {
  name: 'App',
  components: {
    barcodes
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
