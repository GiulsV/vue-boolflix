<template>
  <div class="search-container">
      <input type="text" v-model="searchText">
      <button @click="sendInput()">Cerca</button>
  </div>
</template>

<script>
import axios from 'axios';
// api_key=7d280c404bb1d6acb95e9350180c6a30
export default {
    name: "SearchComp",
    data() {
        return {
            filmApiQuery: "https://api.themoviedb.org/3/search/movie?api_key=7d280c404bb1d6acb95e9350180c6a30&language=it-IT&query=",
            seriesApiQuery: "https://api.themoviedb.org/3/search/tv?api_key=7d280c404bb1d6acb95e9350180c6a30&language=it-IT&query=",
            searchText: "",
            filmList: {
                film: [],
                series: []
            },
        }
    },
    methods: {
        sendInput() {
            axios.get(this.filmApiQuery+this.searchText)       //film
                .then(res => {
                    this.filmList.film = res.data.results;
                    axios.get(this.seriesApiQuery+this.searchText)  //serie TV
                        .then(res => {
                            this.filmList.series = res.data.results;
                            this.$emit("sendSearch", this.filmList);
                        })
                        .catch(err => console.log(err))
                })
                .catch(err => console.log(err))
        }
    }
}
</script>

<style lang="scss" scoped>
</style>