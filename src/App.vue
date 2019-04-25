<template>
  <div id="app">
    <cityPicker></cityPicker>
  </div>
</template>

<script>
import cityPicker from './components/cityPicker'

export default {
  name: 'app',
  components: {
    cityPicker
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
