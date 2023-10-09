<template>
  
  <gestionLivres></gestionLivres>
</template>

<script>
import gestionLivres from './components/gestionLivres.vue'

export default {
  name: 'App',
  components: {
    gestionLivres
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
