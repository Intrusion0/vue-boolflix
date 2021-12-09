<template>
  <main>
    <div class="container-cards">
        <!-- Componente Card -->
        <Card 
        v-for="card, i in filmsAndSeries"
        :key="i"
        :details="card"
        :visibleActors="actorVisible"
        :visibleGenres="genreVisible"
        :genres="allGenres"
        />
    </div>
  </main>
</template>

<script>
import Card from './Card.vue'

export default {
  name: 'Main',
  components: {
      Card,
  },
  props: {
      filmsAndSeries: Array,
      allGenres: Array,
      actorVisible: Boolean,
      genreVisible: Boolean,
  }
}
</script>

<style scoped lang="scss">

main {
    background-color: #141414;
    width: 100%;
    height: calc(100vh - 85px);
    padding: 50px 0;
    overflow: auto;

    &::-webkit-scrollbar {
        width: 6px;
        height: 5px;
        background-color: #141414;
    }

    &::-webkit-scrollbar-thumb {
        background: #4e0004;
    }

    .container-cards {
        display: flex;
        flex-wrap: wrap;
        width: 90%;
        margin: 0 auto;
        padding: 20px 0;
    }
}
</style>
