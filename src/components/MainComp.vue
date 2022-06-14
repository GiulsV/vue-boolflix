<template>
  <main>
    <ul v-for="(film, index) in arrayFilms" :key='index'>
          <li>Titolo: {{film.title}}</li>
          <li>Titolo Originale: {{film.original_title}}</li>
          <li>Lingua Originale: {{film.original_language}}</li>
          <li>Voto: {{film.vote_average}}</li>
    </ul>
  </main>
</template>

<script>

export default {
    name: "MainCompVue",
    props: {
        arrayFilms: Array,
    },

    data() {
        return {
            
        }
    },

    computed: {

    }
    
}
</script>

<style lang="scss" scoped>
ul{
    list-style: none;
}
</style>