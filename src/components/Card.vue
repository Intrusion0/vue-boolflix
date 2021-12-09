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
          <span>
               <flag :iso="getFlags()"/>
          </span>
      </div>
      <div>
          Voto:
          <span>
              {{ (Math.round(details.vote_average / 2) == 0) ? 1 : Math.round(details.vote_average / 2) }}
              <font-awesome-icon icon="star" :class="firstStar(details.vote_average)"/>
              <font-awesome-icon icon="star" :class="secondStar(details.vote_average)"/>
              <font-awesome-icon icon="star" :class="thirdStar(details.vote_average)"/>
              <font-awesome-icon icon="star" :class="fourthStar(details.vote_average)"/>
              <font-awesome-icon icon="star" :class="fifthStar(details.vote_average)"/>
          </span>
      </div>
      <div v-if="details.overview !== ''">
          Overview:
          <span>
              {{ details.overview }}
          </span>
      </div>
      <div>
          <button @click.prevent="getActors" class="btn-actors-genres">Attori</button>
          <span v-if="visibleActors" class="container-actors-genres">
              <ul>
                  <li v-for="actor, j in actors" :key="j">
                      {{ actor }}
                  </li>
              </ul>
          </span>
      </div>
      <div>
          <button @click.prevent="getGenres" class="btn-actors-genres" >Generi</button>
          <span v-if="visibleGenres" class="container-actors-genres">
              <ul class="list-genres">
                  <li v-if="genresCard.length === 0">
                      Nessun genere presente!
                  </li>
                  <li v-else v-for="genre, a in genresCardUnique" :key="a">
                      <span class="container-genres">
                          Genere {{ ++a }}:
                      </span>
                      {{ genre }}
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
      details: Object,
      visibleActors: Boolean,
      visibleGenres: Boolean,
      genres: Array,
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
          genresCard: [],
          genresCardUnique: [],
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
                this.visibleActors = true;

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
                this.visibleActors = true;

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
      },
      getFlags() {
          let countryFlag = '';

          switch (this.details.original_language) {
              case 'en':
                  countryFlag = 'gb'
                break;
              case 'ko':
                countryFlag = 'kr'
                break;
              case 'hi':
                countryFlag = 'in'
                break;
              case 'ja':
                countryFlag = 'cn'
                break;
              case '':
                countryFlag = 'gb'
                break;
              default:
                countryFlag = this.details.original_language;
                break;
          }
          return countryFlag
      },
      firstStar(value) {
        if (Math.round(value / 2) >= 0) {
            return 'checked'
        } else {
            return ''
        }
      },
      secondStar(value) {
        if (Math.round(value / 2) >= 2) {
            return 'checked'
        } else {
            return ''
        }
      },
      thirdStar(value) {
        if (Math.round(value / 2) >= 3) {
            return 'checked'
        } else {
            return ''
        }
      },
      fourthStar(value) {
        if (Math.round(value / 2) >= 4) {
            return 'checked'
        } else {
            return ''
        }
      },
      fifthStar(value) {
        if (Math.round(value / 2) >= 5) {
            return 'checked'
        } else {
            return ''
        }
      },
      getGenres() {
        
        this.allGenre = [];
        this.visibleGenres = true;

          this.genres.forEach(element => {
              this.allGenre.push(element);
          });

          console.log('Tutti i generi: ', this.allGenre);
          console.log('Id genere card: ', this.details.genre_ids);

        this.genresCard = this.allGenre.filter(value => this.details.genre_ids.includes(value.id))

        const map = new Map(this.genresCard.map(value => [value.id, value.name, value]));
        this.genresCardUnique = [...map.values()];

        console.log('Generi card: ', this.genresCardUnique);
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

        .btn-actors-genres {
            height: 35px;
            width: 75px;
            font-size: 18px;
            font-weight: 800;
            color: #ffffff;
            background-color: #99040b;
            border: 0;
            cursor: pointer;
            margin-top: 10px;
        }

        span {
            font-weight: 600;
            font-size: 17px;
            color: #fff;

            &.container-actors-genres {
                display: flex;
                flex-direction: column;
                margin: 10px 0;
                line-height: 30px;

                ul {
                    list-style: circle;
                    margin-left: 20px;
                }

                .list-genres {
                    list-style: none;
                    margin: 0;

                    .container-genres {
                        color:#afafaf;
                        font-size: 19px;
                        margin-right: 5px;
                    }
                }
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
