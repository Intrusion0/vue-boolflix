<template>
  <main>
    <div class="container-cards">
        <!-- Componente Card -->
        <Card 
        v-for="card, i in cards"
        :key="i"
        :details="card"
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
      cards: Array,
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

    .container-cards {
        display: flex;
        flex-wrap: wrap;
        width: 90%;
        margin: 0 auto;
        padding: 20px 0;
    }
}
</style>
