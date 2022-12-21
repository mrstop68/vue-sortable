<template>
  <Simple/>
  <hr>
</template>

<script>
import Simple from './components/simple.vue'

export default {
  name: 'App',
  components: {
    Simple
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-left: 60px;
  padding: 4em;
}
</style>
