<template>
  <div id="app">
    <!-- Componente Header -->
    <Header
    @valueText="movieSearch"
    />
    <!-- Componente Main -->
    <Main
    :cards="cards"
    />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  data() {
    return {
      apiUrl: 'https://api.themoviedb.org/3/search/movie?api_key=',
      apiKeys: 'c4d909d32f7d67d5875e76a887f02111',
      apiLanguage: '&language=it-IT',
      apiPage: '&page=1',
      cards: [],
    }
  },
  methods: {
    movieSearch(value) {
        axios
        .get(this.apiUrl + this.apiKeys + this.apiLanguage + this.apiPage + '&query=' + value)
        .then((result) => {
            this.cards = result.data.results
            console.log(this.cards);
            console.log(value);
        })
        .catch((error) => {
            console.log('Alert! ' + error);
        })
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
