<template>
  <div id="app">
    <QRReader/>
  </div>
</template>

<script>
import QRReader from './components/QRReader.vue'

export default {
  name: 'App',
  components: {
    QRReader
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
