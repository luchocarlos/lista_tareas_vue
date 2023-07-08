<template>
  <ListaTareas/>
</template>

<script>
import ListaTareas from './components/Tareas.vue'

export default {
  name: 'App',
  components: {
    // eslint-disable-next-line no-undef
    ListaTareas
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
