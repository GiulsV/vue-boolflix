<template>
  <div class="card-container">
        <li>
            <img :src="basicImageURL + poster" alt="poster" id="poster">
        </li>
        <div class="info-container">
            <li class="film-info"> <span class="label">Titolo: </span> {{title}}</li>
            <li class="film-info"><span class="label">Titolo originale: </span> {{originalTitle}}</li>
            <li class="film-info"><span class="label">Lingua originale: </span> <img class="flag" :src="getImgUrl()" alt=""></li>
            <li class="film-info">
                <span class="label">Voto: </span>
                <i v-for="(vote,index) in getVoteStar(vote)" :key=index class="fa-solid fa-star rate"></i>
            </li>
            <li class="film-info"> <span class="label">Descrizione: </span> <p>{{overview}}</p></li>
        </div>       
  </div>
</template>


<script>
export default {
    name: "FilmComp",
     data() {
        return {  
            basicImageURL: "https://image.tmdb.org/t/p/w342",
        }
    },
    props: {
        poster: String,
        title: String,
        originalTitle: String,
        language: String,
        vote: Number,
        overview: String
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
        getVoteStar(value) {
            if(value != 0) {
                return Math.round(((Math.round(value)*5)/10));
            }
            else{
                return 1;
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
            // outline-offset: 7px;
            cursor: pointer;
        }
        &:hover .poster {
            // transform: rotate3d(0, 1, 0, 180deg);
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
            transition: .5s ease;
            background-color: rgb(54, 54, 65);
            color: rgb(221, 217, 217);
            padding: 1rem 0.7rem;
            width:100%;
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
