<template>
  <div class="container-cards">
      <div class="card" 
      v-for="card, i in details"
      :key="i">
      <div>
          Titolo:
          <span>
              {{ card.title }}
          </span>
      </div>
      <div>
          Titolo originale:
          <span>
              {{ card.original_title }}
          </span>
      </div>
      <div>
          Lingua:
          <span>
              {{ card.original_language }}
          </span>
      </div>
      <div>
          Voto:
          <span>
              {{ card.vote_average }}
          </span>
      </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
      details: Array
  }
}
</script>

<style scoped lang="scss">

.container-cards {
    display: flex;
    flex-wrap: wrap;
    width: 90%;
    margin: 0 auto;
    padding: 20px 0;

    .card {
        display: flex;
        flex-direction: column;
        width: calc(100% / 5 - 30px);
        margin: 10px 15px;
        padding: 30px 15px;
        background-color: #222222;

        div {
            color: white;
            font-weight: 700;
            margin: 5px 0;

            span {
                font-weight: 400;
            }
        }
    }
}
</style>
