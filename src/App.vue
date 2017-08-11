<template>
  <div id="app">
    <img src="./assets/logo.png">
    <Dexter></Dexter>
  </div>
</template>

<script>
import Dexter from './components/Dexter'

export default {
  name: 'app',
  components: {
    Dexter
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
