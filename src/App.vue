<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <InstantSearch />
  </div>
</template>

<script>
import InstantSearch from './components/InstantSearch.vue'

export default {
  name: 'App',
  components: {
    InstantSearch
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
