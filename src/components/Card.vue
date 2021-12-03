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
              {{ (Math.round(details.vote_average / 2) == 0) ? 1 : Math.round(details.vote_average / 2) }}
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average / 2) >= 0) ? 'checked' : '' "/>
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average / 2) >= 2) ? 'checked' : '' "/>
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average / 2) >= 3) ? 'checked' : '' "/>
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average / 2) >= 4) ? 'checked' : '' "/>
              <font-awesome-icon icon="star" :class="(Math.round(details.vote_average / 2) == 5) ? 'checked' : '' "/>
          </span>
      </div>
      <div v-if="details.overview !== ''">
          Overview:
          <span>
              {{ details.overview }}
          </span>
      </div>
      <div>
          <button @click="getActors" class="btn-actors">Attori</button>
          <span class="container-actors">
              <ul>
                  <li v-for="actor, i in actors" :key="i">
                      {{ actor }}
                  </li>
              </ul>
          </span>
      </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Card',
  props: {
      details: Object
  },
  data() {
      return {
          urlImg: 'https://image.tmdb.org/t/p/',
          imgSize: 'w342',
          apiCredits: 'https://api.themoviedb.org/3/',
          apiKeys: '?api_key=c4d909d32f7d67d5875e76a887f02111',
          apiLanguage: '&language=it-IT',
          actorsFilm: [],
          actorsSerie: [],
          actors: '',
      }
  },
  methods: {
      getActors() {
          if (this.details.original_title) {
            axios // RICHIESTA PER GENERARE SOLO I PRIMI 5 ATTORI DEI FILM
            .get(this.apiCredits + 'movie/' + this.details.id + '/credits' + this.apiKeys + this.apiLanguage)
            .then((result) => {
                this.actorsFilm = result.data.cast;
                
                this.actors = [];

                    switch (this.actorsFilm.length) {
                        case 0:
                            this.actors.push('Nessun attore presente');
                            break;
                        case 1:
                            this.actors.push(this.actorsFilm[0].name);
                            break;
                        case 2:
                            this.actors.push(this.actorsFilm[0].name, this.actorsFilm[1].name);
                            break;
                        case 3:
                            this.actors.push(this.actorsFilm[0].name, this.actorsFilm[1].name, this.actorsFilm[2].name);
                            break;
                        case 4:
                            this.actors.push(this.actorsFilm[0].name, this.actorsFilm[1].name, this.actorsFilm[2].name, this.actorsFilm[3].name);
                            break;
                        case 5:
                            this.actors.push(this.actorsFilm[0].name, this.actorsFilm[1].name, this.actorsFilm[2].name, this.actorsFilm[3].name, this.actorsFilm[4].name);
                            break;
                        default:
                            this.actors.push(this.actorsFilm[0].name, this.actorsFilm[1].name, this.actorsFilm[2].name, this.actorsFilm[3].name, this.actorsFilm[4].name);
                            break;
                    }
                
                console.log(this.actors);
                console.log(this.actorsFilm);
        
                this.actorsFilm = [];
            })
            .catch((error) => {
                console.log('Alert! ' + error);
            })
          } else if (this.details.original_name) {
            axios // RICHIESTA PER GENERARE SOLO I PRIMI 5 ATTORI DELLE SERIE TV
            .get(this.apiCredits + 'tv/' + this.details.id + '/credits' + this.apiKeys + this.apiLanguage)
            .then((result) => {
                this.actorsSerie = result.data.cast

                this.actors = [];

                switch (this.actorsSerie.length) {
                    case 0:
                        this.actors.push('Nessun attore presente');
                        break;
                    case 1:
                        this.actors.push(this.actorsSerie[0].name);
                        break;
                    case 2:
                        this.actors.push(this.actorsSerie[0].name, this.actorsSerie[1].name);
                        break;
                    case 3:
                        this.actors.push(this.actorsSerie[0].name, this.actorsSerie[1].name, this.actorsSerie[2].name);
                        break;
                    case 4:
                        this.actors.push(this.actorsSerie[0].name, this.actorsSerie[1].name, this.actorsSerie[2].name, this.actorsSerie[3].name);
                        break;
                    case 5:
                        this.actors.push(this.actorsSerie[0].name, this.actorsSerie[1].name, this.actorsSerie[2].name, this.actorsSerie[3].name, this.actorsSerie[4].name);
                        break;
                    default:
                        this.actors.push(this.actorsSerie[0].name, this.actorsSerie[1].name, this.actorsSerie[2].name, this.actorsSerie[3].name, this.actorsSerie[4].name);
                        break;
                }

                console.log(this.actors);
                console.log(this.actorsSerie);

                this.actorsSerie = [];
            })
            .catch((error) => {
                console.log('Alert! ' + error);
            })
          }
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

        .btn-actors {
            height: 35px;
            width: 75px;
            font-size: 18px;
            font-weight: 800;
            color: #ffffff;
            background-color: #4e0004;
            border: 0;
            cursor: pointer;
        }

        span {
            font-weight: 600;
            font-size: 17px;
            color: #fff;

            &.container-actors {
                display: flex;
                flex-direction: column;
                margin: 10px 0;
                line-height: 30px;
            }
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
