<template>
  <div id="app">
    <!-- Componente Header -->
    <Header
    @valueText="sendTextActual"
    />
    <!-- Componente Main -->
    <Main
    :searchTextActual="this.searchTextActual"
    />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  data() {
    return {
      searchTextActual: '',
    }
  },
  methods: {
    sendTextActual(value) {
      this.searchTextActual = value;
      console.log(this.searchTextActual);
    }
  }
}
</script>

<style lang="scss">


// General rules
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
