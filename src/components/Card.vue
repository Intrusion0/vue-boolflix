<template>
    <div class="card">
      <div v-if="details.poster_path !== null" class="picture">
          <img :src="urlImg + imgSize + details.poster_path" :alt="details.original_title || details.original_name">
      </div>
      <div v-else class="picture">
          <img src="@/assets/img/img-card-default.png" :alt="details.original_title || details.original_name">
      </div>
      <div>
          Titolo:
          <span>
              {{ details.title || details.name }}
          </span>
      </div>
      <div>
          Titolo originale:
          <span>
              {{ details.original_title || details.original_name }}
          </span>
      </div>
      <div>
          Lingua:
          <span v-if="details.original_language == 'en' ">
               <flag iso="gb"/>
          </span>
          <span v-else-if="details.original_language == 'ko' ">
              <flag iso="kr"/>
          </span>
          <span v-else-if="details.original_language == 'hi' ">
              <flag iso="in"/>
          </span>
          <span v-else-if="details.original_language == '' ">
              <flag iso="it"/>
          </span>
          <span v-else>
               <flag :iso="details.original_language"/>
          </span>
      </div>
      <div>
          Voto:
          <span>
              {{ details.vote_average > 5 ? 5 : Math.round(details.vote_average) }}
          </span>
      </div>
    </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
      details: Object
  },
  data() {
      return {
          urlImg: 'https://image.tmdb.org/t/p/',
          imgSize: 'w342'
      }
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

    .picture {
        width: auto;

        img {
            width: 100%;
        }
    }

    div {
        color: white;
        font-weight: 700;
        margin: 5px 0;

        span {
            font-weight: 400;
        }

        .star:before {
            content: '\2605';
            width: 60px;
            height: 60px;
            font-size: 60px;
        }
    }
}
</style>
