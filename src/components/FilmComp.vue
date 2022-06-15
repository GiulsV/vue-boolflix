<template>
  <div class="card-container">
      <ul>
        <li><img :src="basicImageURL + poster" alt="poster" id="poster"></li>
        <li>Titolo:{{title}}</li>
        <li>Titolo Originale:{{originalTitle}}</li>
        <li>Lingua:<img :src="getImgUrl()" alt="flag" id="flag"></li>
        <li>Voto:{{vote}}</li>
      </ul>
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
        vote: Number
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
            
        }
    }
}
</script>

<style lang="scss" scoped>
ul{
    list-style: none;
}

#flag{
    width: 90px;
    height: 60px;
}
</style>