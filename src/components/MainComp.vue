<template>
  <main>
    <div class="main-container">
        <div v-if="arrayFilms.film.length > 0" class="films-container">

            <h2 class="section" v-if="arrayFilms.film">Film</h2>

            <ul>
                <FilmComp
                    v-for="(film, index) in arrayFilms.film"
                    :key=index+film.id
                    :title="film.title"
                    :originalTitle="film.original_title"
                    :language="film.original_language"
                    :vote="film.vote_average"
                    :poster="film.poster_path"
                    :overview="film.overview.length > 0 ? film.overview : 'No Description'"
                />
            </ul>
        </div>
        <div v-else-if="arrayFilms.firstSearch">
            <h2 class="section">Non sono stati trovati film</h2>
        </div>
    
        <div v-if="arrayFilms.series.length > 0" class="series-container">

            <h2 class="section" v-if="arrayFilms.series">Serie TV</h2>
            <ul>
                <FilmComp
                    v-for="(serie, index) in arrayFilms.series"
                    :key=index+serie.id
                    :title="serie.name"
                    :originalTitle="serie.original_name"
                    :language="serie.original_language"
                    :vote="serie.vote_average"
                    :poster="serie.poster_path"
                    :overview="serie.overview.length > 0 ? serie.overview : 'No Description'"
                />
            </ul>
        </div>
        <div v-else-if="arrayFilms.firstSearch">
            <h2 class="section">Non sono state trovate serie TV</h2>
        </div>
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
    .main-container {
        width: 100%;
        height: calc(100vh - 70px);
        margin: auto;
        padding: 2rem 0;
        background-color: gray;
        .films-container, .series-container {
            
            ul {
                display: flex;
                flex-wrap: wrap;
                margin: 1rem 0 4rem 0;
                gap: 1.5rem;
                list-style-type: none;
            }
        }
        .section {
            margin-left: 50px;
                font-size: 2rem;
                color: white;
                letter-spacing: 2px;
            }
    }

</style>