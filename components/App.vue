<template>
  <div id="app">
    <Navigation />
    <main>
      <router-view />
    </main>
    <Footer />
  </div>
</template>

<script>

import Navigation from './Navigation.vue'
import Footer from './Footer.vue'

export default {
  name: 'App',
  components: {
    Navigation,
    Footer
  },
  data () {
    return {
      var1: []
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #f3e5e5;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  min-height: 80vh;
}
header {
  font-size: 2em;
}
main {
  flex-grow: 1;
}
</style>
