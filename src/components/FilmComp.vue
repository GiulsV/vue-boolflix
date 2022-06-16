<template>
  <div v-if="filmGenres.includes(genreChoice) || genreChoice == null" @mouseover="learnMore()" class="card-container">
        <li>
            <img :src="basicImageURL + poster" alt="poster" id="poster">
        </li>
        <div class="info-container">
            <li class="film-info"> <span class="label">Titolo: </span> {{title}}</li>
            <li class="film-info"><span class="label">Titolo originale: </span> {{originalTitle}}</li>
            <li class="film-info"><span class="label">Lingua originale: </span> <img class="flag" :src="getImgUrl()" alt=""></li>
            <li class="film-info"><span class="label">Voto: </span>
                <i v-for="(vote,i) in getVoteStar(vote)" :key="'A'+ i" class="fa-solid fa-star rate"></i>
                <i v-for="(vote, i) in (5 - getVoteStar(vote))" :key="'B' + i" class="fa-regular fa-star rate"></i>
            </li>
            <!-- <li class="film-info"> <span class="label">Descrizione: </span> <p>{{overview}}</p></li>
        </div>       
  </div> -->
              <transition name="fade">
                <li v-if="!learnMoreClick" class="film-info" key=1>
                    <span class="label">Descrizione:</span>
                    <p class="desc">{{overview}}</p>
                </li>
            </transition>

            <transition name="fade">
                <li v-if="learnMoreClick" class="film-info" key=2> 
                    <span class="label">Cast: </span>
                    <p 
                        v-for="(actor, index) in castName"
                        :key="index"
                        >
                        {{actor}}
                    </p>
                </li>
            </transition>
            <transition name="fade">
            
                <li v-if="learnMoreClick" class="film-info" key=2> 
                    <span class="label">Generi Correlati: </span>
                    <p 
                        v-for="(genre, index) in filmGenresName"
                        :key="index"
                        >
                        {{genre}}
                    </p>
                </li>
            </transition>

        </div>
        <button @click="learnMoreClick = !learnMoreClick">Scopri di più ></button>
        
  </div>
</template>


<script>
import axios from "axios";

export default {
    name: "FilmComp",
     data() {
        return {  
            basicImageURL: "https://image.tmdb.org/t/p/w342",
            baseUrl: "https://api.themoviedb.org/3", 
            apiKey: "7d280c404bb1d6acb95e9350180c6a30",
            castName: [],
            genres: [],
            learnMoreClick: false,
            filmGenresName: []
        }
    },
    props: {
        poster: String,
        title: String,
        originalTitle: String,
        language: String,
        vote: Number,
        overview: String,
        id: Number,
        type: String,
        filmGenres: Array,
        genreChoice: Number
    },
    methods: {
        getImgUrl() {
            switch (this.language) {
                case "it":
                    return require("../assets/img/it.svg");
                case "en":
                    return require("../assets/img/gb.svg");
                case "fr":
                    return require("../assets/img/fr.svg");                    
                case "es":
                    return require("../assets/img/es.svg");
                case "de":
                    return require("../assets/img/de.svg");
                default:
                    return require("../assets/img/xx.svg");
            }
            
        },
        getVoteStar(stars) {
            if(stars >= 0) {
                return Math.round(((Math.round(stars)*5)/10));
            }            
        },
        learnMore() { 
            if(this.castName.length == 0) {
                axios.get(`${this.baseUrl}/genre/${this.type}/list?api_key=${this.apiKey}`)
                    .then(res => {
                        this.genres = res.data.genres;
                        this.transformIdGenres();
                    })
                    .catch(err => console.log(err));
                
                 axios.get(`${this.baseUrl}/${this.type}/${this.id}/credits?api_key=${this.apiKey}`)
                     .then(res => {
                         const castList = res.data.cast;
                         this.castName = [];
                         for(let j = 0; j < 5; j++) {
                             this.castName.push(castList[j].name);
                         }
                     })
                     .catch(err => console.log(err));
                
            }
        
        },
        transformIdGenres() {
            this.filmGenresName = [];
            for(let y=0; y < this.filmGenres.length; y++) {
                for(let i=0; i < this.genres.length; i++) {
                    if(this.genres[i].id == this.filmGenres[y]) {
                        
                        this.filmGenresName.push(this.genres[i].name);
                    }
                }
            }
        }
    }
}
</script>


<style lang="scss" scoped>
    .card-container {
        width: calc(100% / 4 - 1.5rem);
        max-height: 60vh;
        position: relative;
        overflow: hidden;
        transition: all 0.2s;
        &:hover {
            outline: 2px solid white;
            cursor: pointer;
        }
        &:hover .poster {
            filter: brightness(30%);
        }
        &:hover .info-container {
            opacity: 1;
            
        }
        li {
            height: 100%;
        }
        #poster {
            width: 100%;
            height: 100%;
            transition: all 0.5s;
        }
        li.film-info {
            margin: 0.4rem 0;
            p {
                height: 43vh;
                overflow-y: scroll;
                margin-top: 5px;
                -ms-overflow-style: none;
                scrollbar-width: none;
            }
            p::-webkit-scrollbar {
                display: none;
            }
        }
        
        .flag {
            width: 30px;
            vertical-align: sub;
        }
        .info-container {
            position: absolute;
            top: 0;
            left: 0;
            opacity: 0;
            transition: all 1s;
            background-color: rgb(54, 54, 65);
            color: rgb(221, 217, 217);
            padding: 1rem 0.7rem;
            width:100%;
            .fade-enter-active {
                transition: opacity 1s;
            }
            .fade-leave-active {
                transition: opacity 1s;
                display: none;
            }
            .fade-enter,
            .fade-leave-to {
                    opacity: 0;
            }
            .label {
                text-transform: uppercase;
                font-size: 1rem;
                font-weight: bold;
            }
            .rate {
                color: rgb(243, 221, 26);
            }
        }
    }
</style>
