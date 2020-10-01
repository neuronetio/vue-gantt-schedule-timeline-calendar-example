<template>
  <gstc />
</template>

<script>
import GSTCComponent from './components/GSTC.vue'

export default {
  name: 'App',
  components: {
    'gstc':GSTCComponent
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
