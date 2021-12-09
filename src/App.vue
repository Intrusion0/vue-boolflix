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
    :allGenres="getAllGenres"
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
      apiUrl: 'https://api.themoviedb.org/3/',
      apiKeys: '?api_key=c4d909d32f7d67d5875e76a887f02111',
      apiLanguage: '&language=it-IT',
      apiPage: '&page=1', // potrei gestire le pagine! ogni pagina contiene solo 20 cards. Siccome di default è 1, in pagina visualizzerò massimo 20 cards
      films: [],
      series: [],
      filmsGenres: [],
      serieGenres: [],
      visible: true,
    }
  },
  created() {
    this.movieGenres();
    this.seriesGenres();
  },
  computed: {
    getAllRes() {
      return [...this.series, ...this.films]
    },
    getAllGenres() {
      return [...this.filmsGenres, ...this.serieGenres]
    }
  },
  methods: {
    movieSearch(nameFilm) { // Richiesta per generare i film, in base a ciò che abbiamo inserito
        axios
        .get(this.apiUrl + 'search/' + 'movie' + this.apiKeys + this.apiLanguage + this.apiPage + '&query=' + nameFilm)
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
    seriesTvSearch(nameSerie) { // Richiesta per generare le serie TV, in base a ciò che abbiamo inserito
      axios
        .get(this.apiUrl + 'search/' + 'tv' + this.apiKeys + this.apiLanguage + this.apiPage + '&query=' + nameSerie)
        .then((result) => {
            this.series = result.data.results
            this.visible = false;
            console.log(this.series);
            console.log(nameSerie);
        })
        .catch((error) => {
            console.log('Alert! ' + error);
        })
    },
    movieGenres() { // Richiesta per generare tutti i generi dei film
      axios
        .get(this.apiUrl + 'genre/' + 'movie/' + 'list' + this.apiKeys + this.apiLanguage)
        .then((result) => {
          this.filmsGenres = result.data.genres;
          console.log('Generi film: ', this.filmsGenres);
        })
        .catch((error) => {
            console.log('Alert!' + error);
        })
    },
    seriesGenres() { // Richiesta per generare tutti i generi delle serie TV
      axios
        .get(this.apiUrl + 'genre/' + 'tv/' + 'list' + this.apiKeys + this.apiLanguage)
        .then((result) => {
          this.serieGenres = result.data.genres;
          console.log('Generi serie TV: ', this.serieGenres);
        })
        .catch((error) => {
            console.log('Alert!' + error);
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
