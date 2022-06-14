<template>
  <main>
    <FilmComp 
        v-for="(film, index) in arrayFilms"
        :key=index
        :film="film"
    />
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

</style>