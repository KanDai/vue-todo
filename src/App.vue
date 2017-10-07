<template>
  <div id="app">
    <h1>Vue ToDo Sample</h1>
    <todos></todos>
  </div>
</template>

<script>
import Todos from './components/Todos'

export default {
  name: 'app',
  components: {
    Todos
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #333;
  padding: 30px;
}
</style>
