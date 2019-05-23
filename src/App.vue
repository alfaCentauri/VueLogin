<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <login></login>
  </div>
</template>

<script>
import login from './components/login.vue'

export default {
  name: 'app',
  components: {
    login
  }
}
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
}
</style>
