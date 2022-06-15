<template>
  <div class="search-container">
      <input @keyup.enter="sendInput()" type="text" v-model="searchText">
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
                series: [],
                 firstSearch: false
            },
        }
    },
    methods: {
        sendInput() {
            if(this.searchText.trim() != "") {
                axios.get(this.filmApiQuery+this.searchText)       //prima chiamata: film
                .then(res => {
                    
                    this.filmList.firstSearch = true;
                    this.filmList.film = res.data.results;
                    axios.get(this.seriesApiQuery+this.searchText)  //seconda chiamata: serie TV
                        .then(res => {
                            this.filmList.series = res.data.results;
                            this.$emit("sendSearch", this.filmList);
                        })
                        .catch(err => console.log(err))
                })
                .catch(err => console.log(err))
            }
            else{
                this.filmList = {
                    film: [],
                    series: [],
                    firstSearch: false
                };
                this.$emit("sendSearch", this.filmList);
            }
        }
    }
}
</script>

<style lang="scss" scoped>
    .search-container {
        display: flex;
        align-items: center;
        height: 100%;
        input {
            width: 300px;
            height: 40%;
            background-color: rgba(0,0,0,0);
            border: 1px solid white;
            outline: none;
            color: white;
            padding: 0 1rem;
        }
        button {
            height: 40%;
            border: none;
            background-color: red;
            text-transform: uppercase;
            color: white;
            font-size: 0.8rem;
            cursor: pointer;
            padding: 5px;
            margin-left: 5px;
        }
    }

</style>