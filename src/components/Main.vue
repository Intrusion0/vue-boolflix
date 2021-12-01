<template>
  <main>
    <!-- Componente Card -->
    <Card 
    :details="cards"
    />
  </main>
</template>

<script>
import Card from './Card.vue'
import axios from 'axios'

export default {
  name: 'Main',
  components: {
      Card,
  },
  props: {
      searchTextActual: String,
  },
  data() {
      return {
          apiUrl: 'https://api.themoviedb.org/3/search/movie?api_key=',
          apiKeys: 'c4d909d32f7d67d5875e76a887f02111',
          apiLanguage: '&language=it-IT',
          apiPage: '&page=1',
          searchText: this.searchTextActual,
          cards: []
      }
  },
  created() {
      axios
        .get(this.apiUrl + this.apiKeys + this.apiLanguage + this.apiPage + '&query=' + this.searchText)
        .then((result) => {
            this.cards = result.data.results
        })
        .catch((error) => {
            console.log('Alert! ' + error);
        })
  },
  methods: {
    //   movieSearch() {
    //       axios
    //         .get(this.apiUrl + this.apiKeys + this.apiLanguage + this.apiPage + '&query=' + this.searchText)
    //         .then((result) => {
    //             this.cards = result.data.results
    //         })
    //         .catch((error) => {
    //             console.log('Alert! ' + error);
    //         })
    //   }
  }
}
</script>

<style scoped lang="scss">

main {
    background-color: #141414;
    width: 100%;
    height: calc(100vh - 65px);
    padding: 50px 0;
    overflow: auto;
}
</style>
