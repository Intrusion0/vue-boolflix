<template>
    <div class="card">
      <div v-if="details.poster_path !== null" class="picture">
          <img :src="urlImg + imgSize + details.poster_path" :alt="details.original_title || details.original_name">
      </div>
      <div v-else class="picture">
          <img src="@/assets/img/img-card-default.png" :alt="details.original_title || details.original_name">
      </div>
      <div v-if="details.title !== details.original_title || details.name !== details.original_name ">
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
              {{ (details.vote_average > 5) ? 5 : (Math.round(details.vote_average) == 0) ? 1 : Math.round(details.vote_average) }}
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average) >= 0) ? 'checked' : '' "/>
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average) >= 2) ? 'checked' : '' "/>
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average) >= 3) ? 'checked' : '' "/>
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average) >= 4) ? 'checked' : '' "/>
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average) >= 5) ? 'checked' : '' "/>
          </span>
      </div>
      <div v-if="details.overview !== ''">
          Overview:
          <span>
              {{ details.overview }}
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
  },
  methods: {
    //   stars() {
    //       switch (Math.round(this.details.vote_average)) {
    //           case 1:
    //             'checked'
    //           break;
    //           case 2:
    //             'checked'
    //           break;
    //           case 3:
    //             'checked'
    //           break;
    //           case 4:
    //             'checked'
    //           break;
    //           case 5:
    //             'checked'
    //           break;
    //       }
    //   }
  }
}
</script>

<style scoped lang="scss">
.card {
    display: flex;
    flex-direction: column;
    width: calc(100% / 5 - 30px);
    margin: 10px 15px;
    background-color: #222222;
    min-height: 478px;
    max-height: 478px;
    overflow: auto;

    &::-webkit-scrollbar {
        width: 5px;
        height: 8px;
        background-color: #000;
    }

    &::-webkit-scrollbar-thumb {
        background: #4e0004;
    }

    div {
        font-weight: 800;
        font-size: 19px;
        color: #afafaf;
        display: none;

        &.picture {
            height: 100%;
            width: auto;
            display: block;

            img {
                width: 100%;
                height: 100%;
            }
        }

        span {
            font-weight: 600;
            font-size: 17px;
            color: #fff;
        }

        .star:before {
            content: '\2605';
            width: 60px;
            height: 60px;
            font-size: 60px;
        }
    }

    &:hover div {
        display: block;
        margin: 5px 0;
    }

    &:hover div.picture {
        display: none;
    }

    &:hover {
        padding: 30px 15px;
        border-image: linear-gradient(to bottom, #fff8f8, #4e4e4e) 1;
        border-width: 1px;
        border-style: solid;
        background: #090909;
    }
}

.checked {
    color: yellow;
}

</style>
