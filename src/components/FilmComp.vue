<template>
  <div class="card-container">
      <ul>
          <li>Titolo:{{title}}</li>
          <li>Titolo Originale:{{originalTitle}}</li>
          <li>Lingua:<img :src="getImgUrl()" alt=""></li>
          <li>Voto:{{vote}}</li>
      </ul>
  </div>
</template>

<script>
export default {
    name: "FilmComp",
     data() {
        return {  
        }
    },
    props: {
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

img{
    width: 90px;
    height: 60px;
}
</style>