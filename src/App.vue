<template>
  <div id="app">
    <!-- Componente Header -->
    <Header
    @valueText="movieSearch"
    @valueTextSeries="seriesTvSearch"
    />
    <!-- Componente Main -->
    <Main
    :filmsAndSeries="getAllRes"
    :actorVisible="visible"
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
      apiUrl: 'https://api.themoviedb.org/3/search/',
      apiKeys: '?api_key=c4d909d32f7d67d5875e76a887f02111',
      apiLanguage: '&language=it-IT',
      apiPage: '&page=1', // potrei gestire le pagine! ogni pagina contiene solo 20 cards. Siccome di default è 1, in pagina visualizzerò massimo 20 cards
      films: [],
      series: [],
      visible: true,
    }
  },
  computed: {
    getAllRes() {
      return [...this.series, ...this.films]
    }
  },
  methods: {
    movieSearch(nameFilm) {
        axios
        .get(this.apiUrl + 'movie' + this.apiKeys + this.apiLanguage + this.apiPage + '&query=' + nameFilm)
        .then((result) => {
            this.films = result.data.results
            this.visible = false;
            console.log(this.films);
            console.log(nameFilm);
        })
        .catch((error) => {
            console.log('Alert! ' + error);
        })
    },
    seriesTvSearch(nameSerie) {
      axios
        .get(this.apiUrl + 'tv' + this.apiKeys + this.apiLanguage + this.apiPage + '&query=' + nameSerie)
        .then((result) => {
            this.series = result.data.results
            this.visible = false;
            console.log(this.series);
            console.log(nameSerie);
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
