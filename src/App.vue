<template>
  <div id="app">
    <Header/>
    <MapsVisual/>
  </div>
</template>

<script>
import MapsVisual from './components/MapsVisual.vue'
import Header from './components/Header.vue'

export default {
  name: 'App',
  components: {
    MapsVisual,
    Header,
  }
}
</script>

<style>
#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
