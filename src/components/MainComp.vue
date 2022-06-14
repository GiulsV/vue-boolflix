<template>
  <main>
    <div v-if="arrayFilms.film" class="films-container">
    <h3>Film</h3>
        <FilmComp 
            v-for="(film, index) in arrayFilms.film"
            :key=index+film.id
            :title="film.title"
            :originalTitle="film.original_title"
            :language="film.original_language"
            :vote="film.vote_average"
        />
    </div>
    
    <div v-if="arrayFilms.series" class="series-container">
    <h3>Serie TV</h3>
        <FilmComp 
            v-for="(serie, index) in arrayFilms.series"
            :key=index+serie.id
            :title="serie.name"
            :originalTitle="serie.original_name"
            :language="serie.original_language"
            :vote="serie.vote_average"
        />
    </div>
    
    
  </main>
</template>

<script>
import FilmComp from '@/components/FilmComp.vue';

export default {
    name: "MainCompVue",
    components: {
        FilmComp,
    },
    props: {
        arrayFilms: Object,
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

</style>