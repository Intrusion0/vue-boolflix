<template>
    <div class="card">
      <div>
          Titolo:
          <span>
              {{ details.title }}
          </span>
      </div>
      <div>
          Titolo originale:
          <span>
              {{ details.original_title }}
          </span>
      </div>
      <div>
          Lingua:
          <span>
              {{ details.original_language }}
          </span>
      </div>
      <div>
          Voto:
          <span>
              {{ details.vote_average }}
          </span>
      </div>
    </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
      details: Object
  }
}
</script>

<style scoped lang="scss">
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
</style>
