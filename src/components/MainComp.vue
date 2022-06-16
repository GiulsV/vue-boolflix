<template>
  <main>
    <div class="main-container">
        <div v-if="arrayFilms.film.length > 0" class="films-container">

            <h2 @click="test()" class="program" v-if="arrayFilms.film">Film</h2>

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
                    :id="film.id"
                    :type="`movie`"
                    :filmGenres="film.genre_ids"

                    :genreChoice="choice"
                />
            </ul>
        </div>
        <div v-else-if="arrayFilms.firstSearch" class="not_found">
            <h2 >Non sono stati trovati film</h2>
        </div>
    
        <div v-if="arrayFilms.series.length > 0" class="series-container">

            <h2 class="program" v-if="arrayFilms.series">Serie TV</h2>
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
                    :id="serie.id"
                    :type="`tv`"
                    :filmGenres="serie.genre_ids"

                    :genreChoice="choice"
                />
            </ul>
        </div>
        <div v-else-if="arrayFilms.firstSearch" class="not_found">
            <h2 >Non sono state trovate serie TV</h2>
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
        choice: Number
    },
    data() {
        return {
            
        }
    },
        methods: {
        test() {
            console.log(this.arrayFilms.film);
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
        background-color: rgb(41, 41, 46);
        color: rgb(101, 109, 224);
        letter-spacing: 2px;
        letter-spacing: 2px;
        .films-container, 
        .series-container {
            
            background-color: rgb(41, 41, 46);
            padding: 1.2rem 1.2rem;
            
            ul {
                display: flex;
                flex-wrap: wrap;
                padding: 1rem 0 2rem 0;
                gap: 1.5rem;
                list-style-type: none;
                height: 100%;
            }
        }
        .program {
            margin-left: 50px;
            font-size: 2rem;

        }
        .not_found{
            padding: 90px 0 0 100px ;
            font-size: 1.5rem;

        }
    }

</style>